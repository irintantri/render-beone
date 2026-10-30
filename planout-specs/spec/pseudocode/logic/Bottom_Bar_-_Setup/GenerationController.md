/**
 * Node: POST /api/generate (e6f6852d-6df1-4e5d-b42d-82d55cdfcc2d)
 * Triggered by: "Generate ICF" button click (COMPONENTS)
 * 
 * Logic:
 * 1. Receives protocol_id and template_value from the frontend.
 * 2. Initiates a background job to generate the ICF draft.
 * 3. Returns a GenerateJobAccepted schema containing the job_id and protocol_id.
 * 4. Triggers the Parse Document process.
 */
async function handleGenerateICF(request) {
    const { protocol_id, template_value } = request.body;

    // Create a new record in the GenerationJob entity
    const job = await db.GenerationJob.create({
        protocol_id: protocol_id,
        status: "PENDING",
        created_at: new Date()
    });

    // Trigger downstream parsing logic
    await parseDocument(template_value);

    return {
        status: 200,
        body: {
            job_id: job.id,
            protocol_id: job.protocol_id
        }
    };
}

// Notes covered:
// - POST to /api/generate with the protocol ID and template value.
// - The server starts parsing document.
// - This will return the ICF Generate JSON Schema.