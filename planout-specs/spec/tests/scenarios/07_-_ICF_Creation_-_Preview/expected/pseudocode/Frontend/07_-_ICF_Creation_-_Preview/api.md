export const fetchDocument = async (documentId) => {
  // GET /api/documents/{documentId}
  const response = await fetch(`/api/documents/${documentId}`);
  return response.json();
};

export const fetchDocumentSections = async (documentId) => {
  // GET /api/documents/{documentId}/sections
  const response = await fetch(`/api/documents/${documentId}/sections`);
  return response.json();
};

export const publishDocument = async (body) => {
  // POST /api/publish
  const response = await fetch('/api/publish', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(body)
  });
  return response.json();
};