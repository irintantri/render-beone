/**
 * Node: Review Schema (1be77f74-f8b0-48cf-bc6d-fd941354186d)
 * Input: Logic lane "POST /api/reviewers/{id}/act"
 * Action: Update Reviewer status
 */
export const updateReviewerStatus = async (id: string): Promise<Reviewer> => {
  // Happy Path: Update the 'acted' field to true for the given reviewer ID
  const updatedReviewer = await db.reviewer.update({
    where: { id },
    data: { acted: true }
  });
  return updatedReviewer;
  
  // Validation/Error: If ID is not found, throw 404. If DB connection fails, throw 500.
  // Side Effects: Triggers state update in Logic lane.
};
// Notes covered: Reviewer schema definition (id, document_id, name, role, acted), update reviewer status to "acted".

/**
 * Node: Comment Schema (efe9f2de-6942-4fd7-a0ab-c463f8527052)
 * Input: Logic lane "GET /api/comments?documentId=" and "POST /api/comments"
 * Action: Fetch or Persist Comment data
 */
export const fetchCommentsByDocument = async (documentId: string): Promise<Comment[]> => {
  // Happy Path: Retrieve all comments and replies associated with the document_id
  return await db.comment.findMany({
    where: { document_id: documentId },
    orderBy: { timestamp: 'asc' }
  });
  // Empty State: Return empty array [] if no comments exist.
};

export const createComment = async (commentData: Omit<Comment, 'id' | 'timestamp'>): Promise<Comment> => {
  // Happy Path: Validate payload and persist new comment/reply
  // Validation: Ensure comment_text is not empty and status is one of [open, resolved, closed]
  const newComment = await db.comment.create({
    data: {
      ...commentData,
      id: generateUuid(),
      timestamp: new Date()
    }
  });
  return newComment;
  
  // Error: Throw 400 if validation fails.
  // Side Effects: Returns the saved object to the Logic lane for real-time UI updates.
};
// Notes covered: Comment schema definition (id, document_id, section, owner, comment_text, status, parent_id, timestamp), fetch all comments/replies, persist new entry, return saved comment.