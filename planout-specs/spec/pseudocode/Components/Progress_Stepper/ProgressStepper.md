// UI Component for the horizontal progress tracker
// Asset: assets/61238dad-594f-4495-b090-7062b594f51f.svg

COMPONENT ProgressStepper(currentStep, documentId, completedSteps):
    DEFINE steps = ["Setup", "Generate", "Edit & Refine", "Review", "Preview"]
    
    RENDER Container (Horizontal Layout):
        FOR EACH step IN steps:
            DEFINE status = useStepperNavigation.getStepStatus(step, currentStep, completedSteps)
            DEFINE isClickable = useStepperNavigation.isStepClickable(step, completedSteps, documentId)
            
            RENDER StepItem:
                PROPS:
                    label: step
                    state: status
                    onClick: IF isClickable THEN useStepperNavigation.navigateToStep(step, documentId)
                
                // Visual representation based on state
                IF status == "done":
                    SHOW CheckIcon
                ELSE:
                    SHOW StepNumber
                
                IF status == "active":
                    APPLY HighlightStyle