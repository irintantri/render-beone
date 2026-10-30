/**
 * Node: Resolves the template (e30e0610-8a41-456b-8a18-826bece99b9f)
 * Happy Path: Retrieves template metadata from catalog, loads markdown file, parses sections and tokens.
 * Error State: Throws error if template file or reference is missing.
 */
function resolveTemplate(templateId: string) {
    const catalogEntry = catalog.find(t => t.id === templateId); // <!-- MISSING_FIELD: catalog.id -->
    const templateContent = fs.readFileSync(`icf_templates/${catalogEntry.template_ref}.md`); // <!-- MISSING_FIELD: catalog.template_ref -->
    
    const sections = templateContent.split(/## \d+\. .* \{#.*\}/);
    const placeholders = templateContent.match(/\{\{.*?\}\}/g);
    return { sections, placeholders };
}
// Notes covered: Looks up the selected template value in the catalog, finds its template_ref, loads the corresponding ICF markdown template from icf_templates/.md, template parser splits the markdown into sections using ## N. Title {#key} anchors, collects all {{placeholder}} tokens.

/**
 * Node: Resolves the protocol PDF (287dbbe9-2ad4-4307-b323-289d7fb600b2)
 * Happy Path: Locates PDF path from catalog and reads binary data.
 * Error State: Throws error if file path is invalid or file is inaccessible.
 */
function resolveProtocolPdf(protocolId: string) {
    const protocol = catalog.find(p => p.id === protocolId); // <!-- MISSING_FIELD: catalog.id -->
    return fs.readFileSync(protocol.source_pdf); // <!-- MISSING_FIELD: catalog.source_pdf -->
}
// Notes covered: Looks up the protocol in the file-backed catalog, finds its source_pdf field, reads the PDF bytes from protocols/ or samples/.

/**
 * Node: Extracts text from the PDF (2ba53a9b-78b1-46f2-856a-5c6461db436d)
 * Happy Path: Converts PDF binary to raw string.
 */
function extractText(pdfBuffer: Buffer) {
    return pdfParse(pdfBuffer);
}
// Notes covered: Uses pdf-parse to pull raw text from the protocol PDF (and optionally a reference document), local operation (no LLM call).

/**
 * Node: Builds a skeleton (17c8474c-4dba-4ea9-a810-a376e8728472)
 * Happy Path: Maps placeholders to their respective sections.
 */
function buildSkeleton(placeholders: string[], sections: string[]) {
    return placeholders.map(p => ({
        token: p,
        context: sections.filter(s => s.includes(p))
    }));
}
// Notes covered: Creates a map of every placeholder in the template, annotated with which section(s) it appears in (gives the LLM per-field context).

/**
 * Node: Calls the LLM (required) (1abc84b0-0925-4f94-a41f-1bf6810fa95f)
 * Happy Path: Sends context to OpenRouter, receives JSON mapping.
 * Error State: Retries once if JSON is invalid.
 */
async function callLLM(protocolText: string, templateText: string, fieldGuide: any) {
    const prompt = `Extract info from ${protocolText} for template ${templateText} using ${fieldGuide}. Ensure plain language and natural grammatical form.`;
    let response = await openRouter.call(prompt);
    
    try {
        return JSON.parse(response);
    } catch {
        // Retry once
        return JSON.parse(await openRouter.call(prompt));
    }
}
// Notes covered: Sends the protocol text, the full template text, and a field guide to OpenRouter, system prompt instructs model to extract info and write participant-facing plain language, model returns JSON object mapping field names to values, retries once if invalid JSON.

/**
 * Node: Fills the template (d278a8e0-be0b-442d-8ba7-df0903d49943)
 * Happy Path: Replaces tokens with values or default markers.
 */
function fillTemplate(template: string, extractedData: Record<string, string>) {
    return template.replace(/\{\{(.*?)\}\}/g, (match, key) => {
        return extractedData[key] || `[To be completed: ${key}]`;
    });
}
// Notes covered: Replaces every {{placeholder}} in the template with the extracted value, unfilled tokens become visible [To be completed: ] markers.

/**
 * Node: Saves artifacts (25d90573-e989-4ae5-b61a-b84b1ff82fee)
 * Happy Path: Persists files to disk and triggers database storage.
 */
function saveArtifacts(filledTemplate: string, structure: any, results: any) {
    fs.writeFileSync('tmp/icf.md', filledTemplate);
    fs.writeFileSync('tmp/structure.ts', structure);
    fs.writeFileSync('tmp/results.json', JSON.stringify(results));
    
    const sections = filledTemplate.split('\n'); // Simplified split
    store.generateDocument(sections);
}
// Notes covered: Writes the filled ICF markdown to tmp/, proposed structure as a TypeScript module, extraction results as JSON, splits filled template into section rows, calls store.generateDocument() to persist.

/**
 * Node: Document ID (affa3cfd-d536-4eb5-99b1-271818585b43)
 * Happy Path: Generates unique ID.
 */
function generateDocumentId() {
    const year = new Date().getFullYear();
    const random = Math.floor(Math.random() * 900) + 100;
    return `PROTO-${year}-${random}-ICF`;
}
// Notes covered: Generate ICF ID with format PROTO-year-three digit random number-ICF, avoid duplicate ID, increment number avoiding security concern.