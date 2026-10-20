// Shared definitions for consistency
TYPE StepName = "Setup" | "Generate" | "Edit & Refine" | "Review" | "Preview"
TYPE StepStatus = "done" | "active" | "future"

INTERFACE StepperProps:
    currentStep: StepName
    documentId: string | null
    completedSteps: Array<StepName>