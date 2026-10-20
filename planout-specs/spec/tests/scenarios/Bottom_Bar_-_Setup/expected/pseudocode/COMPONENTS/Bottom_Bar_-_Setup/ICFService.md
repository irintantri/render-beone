/**
 * Service: ICFService
 * Description: Handles the API communication for ICF generation lifecycle.
 */

// API Signature: POST /api/icf/generate
// Request Body: { protocolId, referenceIds[], templateId }
// Response: { generationId: string, status: "pending" }

Function initiateGeneration():
    // Logic to call the backend API to start the generation pipeline
    // This triggers the transition to the "04 - ICF Creation - Generate" screen
    response = API.post("/api/icf/generate", {
        protocolId: SetupContext.protocolId,
        referenceIds: SetupContext.referenceIds,
        templateId: SetupContext.templateId
    })
    
    Return response.generationId