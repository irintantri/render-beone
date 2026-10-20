// Logic to handle step state and navigation rules
// Input: currentStep (string), documentId (string|null), completedSteps (Array<string>)

FUNCTION getStepStatus(stepName, currentStep, completedSteps):
    IF stepName == currentStep: RETURN "active"
    IF completedSteps contains stepName: RETURN "done"
    RETURN "future"

FUNCTION isStepClickable(stepName, completedSteps, documentId):
    // "Generate" is transient and never clickable
    IF stepName == "Generate": RETURN FALSE
    
    // Steps requiring documentId
    IF stepName IN ["Edit & Refine", "Review", "Preview"]:
        RETURN (completedSteps contains stepName) AND (documentId IS NOT NULL)
    
    // Default for "Setup"
    RETURN completedSteps contains stepName

FUNCTION navigateToStep(stepName, documentId):
    IF isStepClickable(stepName):
        // Logic to trigger router push to the route associated with stepName
        // Append documentId to URL if required by the route
        ROUTER.push("/creation/" + stepName + (documentId ? "?id=" + documentId : ""))