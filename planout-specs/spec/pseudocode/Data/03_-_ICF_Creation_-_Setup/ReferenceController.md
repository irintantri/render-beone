/**
 * Handles reference document lifecycle for a specific protocol.
 */
class ReferenceController {

  // GET /api/reference?protocolId={protocolId}
  // Retrieves documents associated with a specific protocol
  async getReferencesByProtocol(req, res) {
    const { protocolId } = req.query;
    const docs = await db.ReferenceDocument.findByProtocol(protocolId);
    res.json({ data: docs });
  }

  // POST /api/reference/{protocolId}/upload
  // Uploads a document and returns metadata
  async uploadReference(req, res) {
    const { protocolId } = req.params;
    const fileData = req.body; // Assume multipart/form-data handled by middleware
    
    const newDoc = await db.ReferenceDocument.create({
      protocol_id: protocolId,
      ...fileData,
      uploaded_at: new Date().toISOString()
    });

    res.status(201).json({
      status: "success",
      message: "Document uploaded successfully",
      reference: newDoc
    });
  }
}