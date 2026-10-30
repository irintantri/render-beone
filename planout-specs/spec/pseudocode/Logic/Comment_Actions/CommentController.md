// Node: GET /api/comments?documentId= (9fd86660-bc82-4e40-beb8-e05a1d0cf495)
// Input: Triggered by Comments component (components) mount.
// Logic:
FUNCTION fetchComments(documentId):
    // Fetch all top-level and nested replies in one call
    comments = SELECT * FROM Comment WHERE document_id = documentId
    RETURN comments
    
    // On unmount:
    ON_UNMOUNT:
        CANCEL pending requests
        CLEAR local comment state
// Output: Populates Comment state in Data layer.
// Notes covered: Request to fetch all comments for current document; Fetch top-level and nested replies in single call; Stored in local state; On unmount, cancel requests and clear state to prevent stale data.

// Node: POST /api/comments (1d558dec-3725-49f5-9387-8f72f507db52)
// Input: Triggered by Add Comment (components) submit.
// Logic:
FUNCTION createComment(payload):
    // Payload includes document_id, section, owner, comment_text, parent_id
    VALIDATE payload
    IF valid:
        INSERT INTO Comment (document_id, section, owner, comment_text, parent_id, status, timestamp)
        VALUES (payload.document_id, payload.section, payload.owner, payload.comment_text, payload.parent_id, 'open', NOW())
        RETURN saved comment record
// Output: Persists to Comment entity in Data layer.
// Notes covered: Client sends message payload; Server validates content; Persists record; Returns saved comment for real-time thread update.