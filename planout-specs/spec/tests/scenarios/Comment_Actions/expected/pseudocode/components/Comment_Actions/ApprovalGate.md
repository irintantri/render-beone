component ApprovalGate(reviewers: Reviewer[], openCommentsCount: number) {
    // Node: Approval Gate (2cecf928-1f5f-4d4f-8fa1-9f20adfb1ecb)
    // Asset: assets/a5ff0cd2-c9d0-4705-8f79-eeac4d8d7b9a.svg
    
    state allReviewersActed = reviewers.every(r => r.status === 'acted');
    state canSubmit = (openCommentsCount === 0 && allReviewersActed);

    render() {
        return (
            <Popover>
                {reviewers.map(reviewer => (
                    <div key={reviewer.id}>
                        <span>{reviewer.name} - {reviewer.role} - {reviewer.status}</span>
                        <button onClick={() => API.actAsReviewer(reviewer.id)}>Act</button>
                    </div>
                ))}
                <SubmitForApprovalButton enabled={canSubmit} openCount={openCommentsCount} />
            </Popover>
        );
    }
}
// Notes covered: Display popover at bottom, Enforce open count = 0, Enforce all reviewers acted, List reviewer name/role/status, Display Act button, Update status on click, Submit button activates when conditions met.