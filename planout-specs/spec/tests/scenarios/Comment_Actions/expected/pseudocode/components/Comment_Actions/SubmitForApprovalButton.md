component SubmitForApprovalButton(enabled: boolean, openCount: number) {
    // Node: Submit for Approval (363e4c68-5777-40a3-821f-546bd506beb6)
    
    const label = enabled ? "Submit for Approval" : `Submit for Approval (${openCount} open)`;

    render() {
        return (
            <button 
                disabled={!enabled} 
                onClick={() => API.submitDocumentForApproval()}
            >
                {label}
            </button>
        );
    }
}
// Notes covered: Display Submit for Approval button, Label shows count if open comments exist, Enabled/Click calls POST /api/documents/{documentId}/submit-approval.