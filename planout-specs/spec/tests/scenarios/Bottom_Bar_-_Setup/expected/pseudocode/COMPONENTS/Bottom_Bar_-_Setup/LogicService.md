// Node: POST /api/generate (id: e6f6852d-6df1-4e5d-b42d-82d55cdfcc2d)
// Receives: protocolId, templateId from GenerateICFButton
// Interface to Frontend: Returns ICF Generate JSON Schema
async function generateICF(protocolId, templateId) {
    // Validation: Ensure protocolId and templateId are present
    if (!protocolId || !templateId) {
        throw new Error("Missing required parameters for generation");
    }

    try {
        // Side Effect: Server starts parsing document
        const response = await API.post('/api/generate', {
            protocolId,
            templateId
        });

        // Happy Path: Return JSON schema for the generation pipeline
        return response.data;
    } catch (error) {
        // Error State: Handle parsing failure or network error
        logError("Generation failed", error);
        throw error;
    }
}
// Notes covered:
// 1. POST to /api/generate with protocol ID and template value.
// 2. Server starts parsing document.
// 3. Returns ICF Generate JSON Schema.