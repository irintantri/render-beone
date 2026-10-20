/**
 * Service to handle retrieval of ICF documents and their associated audit trails
 * for the ReviewPage feature.
 */

// Fetches the full document object to populate the ReviewPage center panel
// Maps to: GET /api/documents/:id
async function getDocumentForReview(documentId) {
    // Query DOCUMENT entity by id
    const document = await db.DOCUMENT.findUnique({
        where: { id: documentId }
    });

    if (!document) {
        throw new Error("Document not found");
    }

    return {
        id: document.id,
        protocol_id: document.protocol_id,
        icf_name: document.icf_name,
        icf_version: document.icf_version,
        template: document.template,
        status: document.status,
        content: document.content,
        metadata: document.metadata,
        published_at: document.published_at,
        created_at: document.created_at,
        last_modified: document.last_modified
    };
}

// Fetches the chronological audit trail for the document
// Maps to: GET /api/documents/:id/audit
async function getDocumentAuditTrail(documentId) {
    // Query AUDIT_LOG entity where resource_id matches the document
    const auditLogs = await db.AUDIT_LOG.findMany({
        where: { resource_id: documentId },
        orderBy: { timestamp: 'desc' }
    });

    return auditLogs.map(log => ({
        id: log.id,
        user_id: log.user_id,
        action: log.action,
        timestamp: log.timestamp
    }));
}