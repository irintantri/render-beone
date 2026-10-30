/**
 * Node: GET /api/documents/:id/audit (bc03a18a-a16e-4627-a6e3-15251e27a6b7)
 * Description: Fetches a composed chronological event feed for the Audit Trail tab.
 */
async function getDocumentAuditTrail(req, res) {
    const { id } = req.params;

    // Happy Path:
    // 1. Query AuditLog where resourceId matches the provided Document.id.
    // 2. Sort the results by timestamp in descending order (newest to oldest).
    const auditLogs = await db.AuditLog.findMany({
        where: { resourceId: id },
        orderBy: { timestamp: 'desc' }
    });

    // 3. Return the list of audit entries to the frontend.
    return res.status(200).json(auditLogs);

    // Validation/Error States:
    // - If no document exists with the provided id, return 404.
    // - If the database query fails, return 500.
    
    // Empty State:
    // - If no audit logs exist for the document, return an empty array [].
}

// Notes covered:
// - The Audit Trail tab on the ReviewPage fetches a composed chronological event feed via the document audit endpoint.
// - Presenting a full history of actions taken on the document in the order they occurred.