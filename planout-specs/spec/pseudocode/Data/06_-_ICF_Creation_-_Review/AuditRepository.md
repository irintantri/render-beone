/**
 * Node: Audit Schema (8b25d9fc-7394-4b7b-a545-d62006dc53f2)
 * Handles the retrieval of chronological activity logs for a specific document.
 */

// Interface for the Logic swimlane: GET /api/documents/:id/audit
// Input: documentId (uuid)
// Output: Array<AuditLogEntry>
interface AuditLogEntry {
  userId: string;
  action: string;
  timestamp: string;
  resourceId: string;
}

/**
 * Implementation of "GET /api/documents/:id/audit" (bc03a18a-a16e-4627-a6e3-15251e27a6b7)
 * Fetches audit logs from the database, sorted by timestamp descending.
 */
async function getDocumentAuditTrail(documentId: string): Promise<AuditLogEntry[]> {
  // Query: SELECT * FROM AuditLog WHERE resourceId = :documentId ORDER BY timestamp DESC
  // Logic: The data is returned as a chronological timeline (newest to oldest).
  return db.auditLogs.findMany({
    where: { resourceId: documentId },
    orderBy: { timestamp: 'desc' }
  });
}

// Happy Path: Returns a sorted array of AuditLogEntry objects.
// Validation: Ensures all fields (userId, action, timestamp, resourceId) are present.
// Empty State: Returns an empty array [] if no logs exist for the resource.
// Side Effects: None.
// Notes covered: Audit Trail tab, log activity user feed, JSON format, chronological timeline, newest to oldest, machine-readable fields (userId, action, timestamp, resourceId).