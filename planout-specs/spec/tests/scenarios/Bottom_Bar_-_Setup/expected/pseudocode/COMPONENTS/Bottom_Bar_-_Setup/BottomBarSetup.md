/**
 * Component: BottomBarSetup
 * Description: A persistent bottom action bar for the Setup page.
 * Asset: assets/4d72f464-245d-49a0-b712-dffa9b8c36bb.svg
 */

Component BottomBarSetup(props):
    // State derived from parent Setup page context
    isProtocolSelected = props.isProtocolSelected
    hasReferences = props.referencesCount > 0
    isTemplateSelected = props.isTemplateSelected
    
    // Derived state for button activation
    canGenerate = isProtocolSelected AND hasReferences AND isTemplateSelected
    
    // Navigation handlers
    handleBackToDashboard = () => navigate("/dashboard")
    handleGenerateICF = () => {
        if (canGenerate) {
            // Trigger generation logic and navigate to progress screen
            ICFService.initiateGeneration()
            navigate("/icf-creation-generate")
        }
    }

    Render:
        Container (BottomBarLayout):
            // Left side: Navigation
            Button (Ghost, Icon: LeftChevron, Label: "Back to Dashboard")
                OnClick: handleBackToDashboard
            
            // Right side: Primary Action
            Button (Primary, Label: "Generate ICF", Disabled: NOT canGenerate)
                OnClick: handleGenerateICF