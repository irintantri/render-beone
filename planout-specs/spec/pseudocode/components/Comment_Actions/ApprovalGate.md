// Bottom popover enforcing submission rules
Component ApprovalGate(documentId, openCommentCount):
    state reviewers = useFetchReviewers(documentId)
    state allReviewed = reviewers.every(r => r.hasActed)
    state canSubmit = (openCommentCount == 0 && allReviewed)

    Render:
        Popover:
            List:
                For each reviewer in reviewers:
                    ReviewerRow(reviewer)
                    Button("Act") -> API.updateReviewerStatus(reviewer.id)
            
            SubmitButton(documentId, canSubmit, openCommentCount):
                Label = canSubmit ? "Submit for Approval" : "Submit for Approval ({openCommentCount} open)"
                OnClick = canSubmit ? API.submitForApproval(documentId) : null
                Disabled = !canSubmit