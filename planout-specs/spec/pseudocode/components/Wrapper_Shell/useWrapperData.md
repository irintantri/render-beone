// Logic Layer: Manages the state and data requirements for the Wrapper Shell.
// This provides the API signature for the frontend components.

function useWrapperData(protocolId: string, icfName: string, icfVersion: string, currentStep: number) {
    // Logic for Node: Functionality (059b1de5-33c6-44c8-bda4-291fca007428)
    // Requirement: Wraps every page inside the five-step creation flow (steps 0–4).
    // Requirement: Provides consistent outer chrome: TopBar, breadcrumb sub-bar, and step indicator.
    
    const validateStep = (step: number) => {
        if (step < 0 || step > 4) throw new Error("Invalid step: Must be between 0 and 4");
    };

    return {
        breadcrumbData: {
            showDashboard: true,
            label: "Consent Creation",
            protocolId,
            icfName,
            icfVersion
        },
        stepIndicator: {
            currentStep,
            totalSteps: 5
        }
    };
}
// Notes covered: Wraps every page inside the five-step creation flow (steps 0–4), Provides consistent outer chrome: TopBar, breadcrumb sub-bar, and step indicator.