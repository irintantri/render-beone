/**
 * Node: Document chunking (e0968a1d-4186-445d-a57e-baaac3ec42e9)
 * Receives: Raw text structure from "Parse Document" (FRONTEND)
 * Action: Retrieves OPENROUTER_API_KEY from environment. 
 *         Initializes LLM connection via OpenAI-compatible interface.
 *         Parses document into logical sections based on structure.
 * Next: "Generate Document via OpenRouter API" (LOGIC)
 * Notes covered: Get the default LLM from the .env file with OPENROUTER_API_KEY as a key. Load the document into the LLM OpenAI in Compatible API and then parse the document by the section. Use the referenced prompt for processing. Once they are processed, move to the next step.
 */
async function chunkDocument(rawDocumentData: any) {
    const apiKey = process.env.OPENROUTER_API_KEY;
    // Logic: Parse document by section using referenced prompt
    const sections = await parseSections(rawDocumentData);
    return sections;
}

/**
 * Node: Generate Document via OpenRouter API (a9429ed2-cb73-473d-a393-4d84ead0af79)
 * Receives: Sections from "Document chunking" (LOGIC) and instructions from "User Input and Instruction Selection" (FRONTEND)
 * Action: 
 *   1. Load PDF file (fs.readFileSync or fetch).
 *   2. Encode to base64 string.
 *   3. Initialize OpenAI client with baseURL "https://openrouter.ai/api/v1".
 *   4. For each document, send message with role "user", content type "file" (base64) and "text" (instruction).
 *   5. Use model "google/gemini-pro-1.5" or similar file-compatible model.
 *   6. Extract summary from response.choices[0].message.content.
 * Next: "raw JSON openrouter" (DATA) and "Sections JSON" (DATA)
 * Notes covered: Integrate with the OpenRouter API using the official HTTP interface; LOAD the PDF file; ENCODE it to a base64 string; INITIALIZE the OpenAI-compatible client; FOR EACH document, build and send a message; Send via client.chat.completions.create; Extract the summary; RETURN all summaries once every document has been processed.
 */
async function generateDocument(sections: any[], instruction: string, fileBuffer: Buffer) {
    const base64Pdf = fileBuffer.toString("base64");
    
    const client = new OpenAI({
        baseURL: "https://openrouter.ai/api/v1",
        apiKey: process.env.OPENROUTER_API_KEY
    });

    const results = [];
    for (const section of sections) {
        const response = await client.chat.completions.create({
            model: "google/gemini-pro-1.5",
            messages: [
                {
                    role: "user",
                    content: [
                        { type: "file", file: { data: base64Pdf, mime_type: "application/pdf" } },
                        { type: "text", text: instruction }
                    ]
                }
            ]
        });
        
        const summary = response.choices[0].message.content;
        results.push({ title: section.title, content: summary });
    }

    // Persist to DATA swimlane
    await saveToDocumentGeneration(results); // <!-- MISSING_FIELD: DocumentGeneration.values -->
    await saveToDocumentSection(results);
    
    return results;
}