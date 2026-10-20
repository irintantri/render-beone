/**
 * Manages reference document lifecycle (fetch from DMS or local upload).
 */
async function fetchReferenceDocuments(protocolId) {
  if (!protocolId) throw new Error("Protocol must be selected");
  // GET /api/reference?protocolId={protocolId}
  return await api.get(`/api/reference?protocolId=${protocolId}`);
}

async function uploadReferenceDocument(protocolId, file, docKind) {
  const formData = new FormData();
  formData.append('file', file);
  formData.append('doc_kind', docKind);
  
  // POST /api/reference/{protocolId}/upload
  return await api.post(`/api/reference/${protocolId}/upload`, formData, {
    headers: { 'Content-Type': 'multipart/form-data' }
  });
}