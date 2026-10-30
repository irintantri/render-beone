/**
 * Cross-lane interface for Logic swimlane: GET /api/documents/:id
 */
export const fetchDocument = async (id: string): Promise<Document> => {
  const response = await fetch(`/api/documents/${id}`);
  if (!response.ok) throw new Error("Failed to load document");
  return response.json();
};

// Notes covered:
// - On load of the page GET /api/documents/:id
// - Loads document metadata and full document object (icf_name, protocol_id, status, created_at, last_modified)
// - Display documents and sections on center panel
// - Primary read endpoint for screen