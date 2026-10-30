/**
 * Component: BottomBar
 * Asset: assets/4d72f464-245d-49a0-b712-dffa9b8c36bb.svg
 */

// Node: Generate ICF (id: 004a64ca-948f-447e-860b-a0b8e194b052)
// Receives: State from parent (protocolSelected, referencesCount, templateSelected)
// Interface to Logic: POST /api/generate(protocolId, templateId)
function GenerateICFButton(props) {
    const isEnabled = props.protocolSelected && props.referencesCount >= 1 && props.templateSelected;

    const handleClick = async () => {
        if (isEnabled) {
            // Transition: "Clicking the button when enabled will generate the ICF draft."
            const response = await LogicService.generateICF(props.protocolId, props.templateId);
            
            // Transition: "The frontend navigates to ICF Creation - Generate."
            Navigation.push('/icf-creation-generate', { schema: response });
        }
    };

    return (
        <Button 
            disabled={!isEnabled} 
            onClick={handleClick}
        >
            Generate ICF
        </Button>
    );
}
// Notes covered: 
// 1. Button becomes active when protocol selected, >=1 references attached, template selected.
// 2. Clicking enabled button generates ICF draft.
// 3. Frontend navigates to ICF Creation - Generate.

// Node: Back to Dashboard (id: a226a6cd-0afe-4865-8287-1c6b8bee8e8a)
function BackToDashboardButton() {
    return (
        <GhostButton 
            icon="left-chevron" 
            onClick={() => Navigation.navigate('/dashboard')}
        >
            Back to Dashboard
        </GhostButton>
    );
}
// Notes covered:
// 1. Display "Back to Dashboard" ghost button with left chevron on left side.
// 2. Clicking navigates to /dashboard.