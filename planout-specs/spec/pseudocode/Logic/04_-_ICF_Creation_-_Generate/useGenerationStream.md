/**
 * Custom hook to manage the SSE connection for ICF generation.
 * Handles the lifecycle of the generation job and triggers navigation upon completion.
 */
FUNCTION useGenerationStream(jobId: string):
  - currentStep: string (The label of the active checkpoint)
  - progress: number (0-100)
  - isComplete: boolean

  INITIALIZE state:
    - currentStep = "Initializing"
    - progress = 0
    - isComplete = FALSE

  ON MOUNT:
    - CREATE EventSource connection to "/api/icf/generation/" + jobId
    
    - ON message RECEIVED:
        - PARSE event data into { status, progress, step_label, document_id }
        - UPDATE progress state
        - UPDATE currentStep state
        
        - IF status == "complete":
            - CLOSE EventSource connection
            - SET isComplete = TRUE
            - WAIT 700ms
            - NAVIGATE to "/edit/" + document_id

    - ON error:
        - LOG error
        - CLOSE EventSource connection

  RETURN { currentStep, progress, isComplete }