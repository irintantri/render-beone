/**
 * Fetches the full document state including content and metadata for the review interface.
 */
FUNCTION getDocumentById(id: UUID): DOCUMENT {
    RETURN DB.query("SELECT * FROM DOCUMENT WHERE id = ?", [id]);
}

/**
 * Retrieves the chronological audit trail for a specific document.
 * Ordered by timestamp descending to show the most recent feedback/actions first.
 */
FUNCTION getAuditLogsByDocumentId(id: UUID): LIST<AUDIT_LOG> {
    RETURN DB.query(
        "SELECT * FROM AUDIT_LOG WHERE resource_id = ? ORDER BY timestamp DESC", 
        [id]
    );
}