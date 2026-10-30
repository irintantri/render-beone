/**
 * Node: POST /api/documents/:id/submit-approval (3d552197-52e2-4a2a-b99f-bfbf5bc859f2)
 * 
 * Receives request from: Submit for Review (components)
 * Sends output to: Submission Document Schema (Data)
 */
async function submitDocumentForReview(req: Request, res: Response) {
    const { id } = req.params;

    // 1. Process document submission
    // 2. Update Document.status to "In Review"
    const updatedDocument = await db.Document.update({
        where: { id: id },
        data: { 
            status: "In Review" 
        }
    });

    // Happy Path: Return the updated document object matching the DocumentDTO schema
    if (updatedDocument) {
        return res.status(200).json(updatedDocument);
    }

    // Error State: Document not found
    return res.status(404).json({ error: "Document not found" });
}

/**
 * Notes covered:
 * - The system processes the document submission.
 * - Automatically updates the document status to In Review once the request is received.
 */