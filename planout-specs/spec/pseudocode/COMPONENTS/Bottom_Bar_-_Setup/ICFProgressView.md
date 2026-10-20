/**
 * Component: ICFProgressView
 * Description: Real-time progress visualization for the generation pipeline.
 * Corresponds to node: 04 - ICF Creation - Generate
 */

Component ICFProgressView():
    // Hook into the generation status stream
    progress = useGenerationProgress(generationId)
    
    Effect:
        If progress.isComplete:
            navigate("/icf-editor")
            
    Render:
        Display 6-step progress tracker based on progress.checkpoints
        If progress.isError:
            Show error notification and allow retry