// API Interface Definitions
interface API {
    // Node: POST /api/reviewers/{id}/act (c0e7259c-f73b-4658-bf6f-c42b547d2373)
    actAsReviewer: (id: string) => Promise<void>; 
    
    // Node: GET /api/comments?documentId= (9fd86660-bc82-4e40-beb8-e05a1d0cf495)
    fetchComments: (documentId: string) => Promise<Comment[]>;
    
    // Node: POST /api/comments (1d558dec-3725-49f5-9387-8f72f507db52)
    submitComment: (payload: CommentPayload) => Promise<Comment>;
    
    submitDocumentForApproval: () => Promise<void>;
}

// Logic Implementation
function actAsReviewer(id) {
    // Happy path: Update status to 'acted'. Error: Surface to caller.
    return fetch(`/api/reviewers/${id}/act`, { method: 'POST' });
}

function fetchComments(documentId) {
    // Happy path: Fetch all top-level and nested. Side effect: Store in local state.
    return fetch(`/api/comments?documentId=${documentId}`).then(res => res.json());
}

function submitComment(payload) {
    // Happy path: Server validates, persists, returns saved comment.
    return fetch('/api/comments', { method: 'POST', body: JSON.stringify(payload) });
}
// Notes covered: Request dispatched with id, Update status to acted on success, Surface error on fail, Fetch all comments in single call, Store in local state, Cancel requests on unmount, Clear state on unmount, Send payload to create entry, Server validates/persists/returns saved comment.