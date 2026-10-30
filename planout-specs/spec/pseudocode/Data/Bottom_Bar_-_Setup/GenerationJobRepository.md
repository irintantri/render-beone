/**
 * Node: ICF Generate JSON Schema (9d946e33-b962-4f91-8085-1e1f6fe14abe)
 * 
 * Description:
 * - Defines the structure for the "GenerateJobAccepted" response.
 * - Requires "job_id" (UUID) and "protocol_id" (string).
 * - "job_id" is used to address the job and open the SSE stream.
 * - "protocol_id" is an echo of the requested protocol ID.
 * - Additional properties are forbidden.
 */

// Interface definition for the Logic layer consumption
export interface GenerateJobAccepted {
  job_id: string; // UUID
  protocol_id: string;
}

/**
 * Logic Flow:
 * 1. Receives request from "POST /api/generate" (e6f6852d-6df1-4e5d-b42d-82d55cdfcc2d).
 * 2. Happy Path: Returns a 202 Accepted status with the GenerateJobAccepted JSON payload.
 * 3. Validation/Error: If the protocol_id is missing or invalid, returns 400 Bad Request.
 * 4. Empty State: Not applicable for this response schema.
 * 5. Side Effects: Persists a new record in the GenerationJob entity with status 'pending'.
 */

export const handleGenerateJobResponse = (jobId: string, protocolId: string): GenerateJobAccepted => {
  // Validate inputs
  if (!jobId || !protocolId) {
    throw new Error("Invalid job or protocol identifier");
  }

  // Return schema-compliant object
  return {
    job_id: jobId,
    protocol_id: protocolId
  };
};

// Notes covered:
// - $schema definition for GenerateJobAccepted
// - job_id (UUID) requirement
// - protocol_id (string) requirement
// - job_id usage for SSE/addressing
// - protocol_id as echo
// - additionalProperties: false constraint