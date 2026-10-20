// API Logic Layer
Service CommentService:
    // POST /api/comments
    Function postComment(documentId, text, sectionId):
        return HTTP.post("/api/comments", { documentId, text, sectionId })

    // PATCH /api/comments/{commentId}
    Function updateCommentStatus(commentId, status):
        return HTTP.patch("/api/comments/{commentId}", { status })

    // POST /api/documents/{documentId}/submit-approval
    Function submitForApproval(documentId):
        return HTTP.post("/api/documents/{documentId}/submit-approval")

    // PATCH /api/reviewers/{reviewerId}
    Function updateReviewerStatus(reviewerId):
        return HTTP.patch("/api/reviewers/{reviewerId}", { status: "acted" })

// Asset Reference:
// The CommentPanel and its sub-components map to the structure defined in:
// Asset: assets/a5ff0cd2-c9d0-4705-8f79-eeac4d8d7b9a.svg