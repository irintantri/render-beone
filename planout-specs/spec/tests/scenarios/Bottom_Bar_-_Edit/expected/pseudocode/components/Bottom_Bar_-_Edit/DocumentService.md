/**
 * Service: DocumentService
 * Purpose: Handles API communication for document lifecycle transitions.
 */

Service DocumentService {

    /**
     * API Signature: POST /api/documents/{documentId}/submit-review
     * Transitions document status from 'Draft' to 'In Review'.
     */
    Async Function submitForReview(documentId) {
        Endpoint = "/api/documents/" + documentId + "/submit-review";
        
        Response = await HttpClient.post(Endpoint, {
            headers: { "Content-Type": "application/json" }
        });

        Return {
            success: Response.status == 200,
            data: Response.body
        };
    }
}