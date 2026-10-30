// Node ID: bc65625b-4ac8-4078-9175-05f549c48f51
// Title: 03 - ICF Creation - Setup
component ICFSetupWizard(props: { protocol_id: string }) {
    /* 
       Input: Receives protocol_id from "Back to Setup" (a9dff811-9b5e-4aa4-9e07-9799a76761ae)
       via navigation path "/setup/{protocol_id}".
    */

    // Requirement: Three-column wizard for configuring a new ICF.
    // Requirement: Select a protocol.
    // Requirement: Attach reference documents.
    // Requirement: Choose a template.
    // Requirement: Launch AI generation.

    // Happy Path: Render the three-column layout and manage wizard state transitions.
    // Validation/Error: Ensure protocol is selected before allowing "Launch AI" action.
    // Empty State: Default columns to empty selection states.
    // Side Effects: Updates local state for wizard progress; triggers AI generation service on launch.

    render() {
        return (
            <WizardLayout>
                <Column1 title="Select Protocol" />
                <Column2 title="Attach Documents" />
                <Column3 title="Choose Template" />
                <ActionFooter onLaunchAI={handleLaunchAI} />
            </WizardLayout>
        );
    }
}
// Notes covered: Three-column wizard for configuring a new ICF, select a protocol, attach reference documents, choose a template, launch AI generation.