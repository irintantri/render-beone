/**
 * Main component logic for the generation progress view.
 */
COMPONENT GenerationProgressView(jobId):
  - IMPORT useGenerationStream hook
  - { currentStep, progress } = useGenerationStream(jobId)

  RENDER:
    - Display progress bar with value = progress
    - Display list of 6 sequential checkpoints
    - Highlight checkpoint matching currentStep
    - IF progress < 100:
        - Show "Generating your ICF..." status text
    - ELSE:
        - Show "Finalizing..." status text