/**
 * Node: GET /api/documents/:id (5ec86318-9c0d-4443-965f-dc8ba509bc60)
 * 
 * Description:
 * - On load of the page, trigger GET /api/documents/:id.
 * - Loads document metadata and returns the full Document object.
 * - Includes fields: icf_name, protocol_id, status, created_at, and last_modified.
 * - Serves as the primary read endpoint for the document display screen.
 * 
 * Previous Nodes:
 * - Document Section Cards (Frontend): Receives request to fetch document data to populate section cards.
 * 
 * Next Nodes:
 * - Document Data Schema (Data): Queries the Document entity to retrieve the full record.
 */

async function getDocumentById(req, res) {
    const { id } = req.params;

    // Happy Path: Fetch document from database
    const document = await db.Document.findUnique({
        where: { id: id }
    });

    if (!document) {
        // Error State: Document not found
        return res.status(404).json({ error: "Document not found" });
    }

    // Return full document object as defined in Document schema
    return res.status(200).json({
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
    });
}

// Notes covered:
// - On load of the page GET /api/documents/:id
// - Loads document metadata and returns the full document object
// - Includes icf_name, protocol_id, status, created_at, and last_modified timestamps
// - Display the documents and sections on the center panel
// - This is the primary read endpoint for any screen that needs to display the document