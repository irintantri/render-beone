import { OpenAI } from 'openai';

/**
 * Initializes the OpenRouter client using the OpenAI SDK.
 * Base URL is pointed to OpenRouter's API endpoint.
 */
const getOpenRouterClient = () => {
  return new OpenAI({
    baseURL: "https://openrouter.ai/api/v1",
    apiKey: process.env.OPENROUTER_API_KEY,
  });
};

/**
 * Processes document generation by interacting with the LLM.
 * 1. Loads file data.
 * 2. Sends to OpenRouter for processing based on template/values.
 * 3. Persists results to DocumentGeneration and DocumentSection entities.
 */
export async function processDocumentGeneration(
  templateId: string, 
  filename: string, 
  values: any
) {
  const client = getOpenRouterClient();
  const model = process.env.DEFAULT_LLM_MODEL || "google/gemini-pro-1.5";

  // 1. Load and encode file
  const fileBuffer = await loadFile(filename); // Helper to read from disk/URL
  const base64Pdf = fileBuffer.toString("base64");

  // 2. Construct prompt context
  const messages = [
    {
      role: "user",
      content: [
        { type: "file", file: { data: base64Pdf, mime_type: "application/pdf" } },
        { type: "text", text: `Generate document content using template ${templateId} and values ${JSON.stringify(values)}` }
      ]
    }
  ];

  // 3. Call OpenRouter
  const response = await client.chat.completions.create({
    model: model,
    messages: messages
  });

  const generatedContent = response.choices[0].message.content;

  // 4. Persist to Database
  const doc = await db.DocumentGeneration.create({
    template_id: templateId,
    source_filename: filename,
    model: model,
    values: values,
    filled_markdown: generatedContent,
    created_at: new Date()
  });

  // 5. Parse sections and store in DocumentSection
  const sections = parseMarkdownToSections(generatedContent);
  for (const section of sections) {
    await db.DocumentSection.create({
      document_id: doc.id,
      title: section.title,
      content: section.content
    });
  }

  return doc;
}