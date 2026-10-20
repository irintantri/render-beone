/**
 * Orchestrates the retrieval of the document and its associated audit history.
 * Used by the ReviewPage to populate the editor and the activity feed.
 */
FUNCTION getReviewData(documentId: UUID): OBJECT {
    document = getDocumentById(documentId);
    auditTrail = getAuditLogsByDocumentId(documentId);
    
    RETURN {
        document: document,
        auditTrail: auditTrail
    };
}

/**
 * Updates the document content and metadata based on reviewer feedback.
 * Updates the last_modified timestamp to reflect the latest iteration.
 */
FUNCTION updateDocumentContent(documentId: UUID, newContent: STRING, newMetadata: JSON): DOCUMENT {
    RETURN DB.execute(
        "UPDATE DOCUMENT SET content = ?, metadata = ?, last_modified = NOW() WHERE id = ?",
        [newContent, newMetadata, documentId]
    );
}