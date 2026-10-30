/**
 * Node: GET /api/documents/:id (25bc464c-e662-40cb-b6c9-f7e63c6c26d4)
 * Logic: Primary read endpoint for document metadata and content.
 */
async function getDocument(req, res) {
    const { id } = req.params;

    // Fetch full document object
    const document = await db.Document.findUnique({
        where: { id: id }
    });

    if (!document) {
        return res.status(404).json({ error: "Document not found" });
    }

    // Returns icf_name, protocol_id, status, created_at, last_modified, etc.
    return res.status(200).json(document);
}

// Notes covered:
// - Loads document metadata and returns the full document object.
// - Includes icf_name, protocol_id, status, created_at, and last_modified.
// - Primary read endpoint for displaying document and sections.

<!-- API_PAYLOAD
{
  "GET /api/documents/:id/audit": {
    "request": {
      "params": [
        { "name": "id", "type": "uuid", "source": "Document.id" }
      ]
    },
    "responses": {
      "200": { "body": ["id", "userId", "action", "timestamp", "resourceId"], "from": "AuditLog" },
      "404": { "body": ["error"] }
    }
  }
}
-->