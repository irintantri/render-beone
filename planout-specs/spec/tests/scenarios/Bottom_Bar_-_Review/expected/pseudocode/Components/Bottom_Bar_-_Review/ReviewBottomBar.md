/**
 * Component: ReviewBottomBar
 * Asset: assets/51f28719-6e79-4309-8c86-767cbbd45bf3.svg
 */

// Node: Submit for Approval (id: a02772c9-5114-4e00-b84d-8ffcbf85ed9e)
// Inputs: documentId (prop), openCommentsCount (prop)
// Outputs: Triggers API call to Logic swimlane
function SubmitForApprovalButton({ documentId, openCommentsCount }) {
    const label = openCommentsCount > 0 
        ? `Submit for Approval (${openCommentsCount} open)` 
        : "Submit for Approval";

    const handleClick = async () => {
        // Cross-lane seam: POST /api/documents/{documentId}/submit-approval
        const response = await API.post(`/api/documents/${documentId}/submit-approval`);
        
        if (response.status === 200) {
            // Navigate to Preview
            router.push('/preview');
        }
    };

    return (
        <button onClick={handleClick} disabled={isLoading}>
            {label}
        </button>
    );
}
// Notes covered: Display Submit for Approval button, If there are open comments the button label shows the count, When enabled and clicked calls POST /api/documents/{documentId}/submit-approval

// Node: Back to Edit (id: bf61a7e8-c3f6-4c40-bcd9-b8b79899bf6b)
// Inputs: None
// Outputs: Navigation event to Edit page
function BackToEditButton() {
    const handleNavigate = () => {
        // Connection: "Edit page"
        router.push('/edit-refine');
    };

    return <button onClick={handleNavigate}>Back to Edit</button>;
}
// Notes covered: Clicking Back to Edit button navigates user to Edit page