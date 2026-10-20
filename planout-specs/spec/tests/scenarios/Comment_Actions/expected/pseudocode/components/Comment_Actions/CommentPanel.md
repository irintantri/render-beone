// Main container for the right-hand side panel
Component CommentPanel(documentId):
    state comments = useFetchComments(documentId)
    state openCommentCount = calculateOpenComments(comments)

    Render:
        ScrollableContainer:
            For each comment in comments:
                CommentCard(comment)
        
        PinnedComposer(documentId):
            OnSubmit(text, sectionId) -> API.postComment(documentId, text, sectionId)
        
        ApprovalGate(documentId, openCommentCount)