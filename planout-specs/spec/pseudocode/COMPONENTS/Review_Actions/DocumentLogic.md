// Node: GET api/documents/{id}/versions (id: 99f93525-070d-48b9-82a6-407dfff58fd5)
// Input: documentId from Components
// Output: Array of version objects to Components
async function fetchDocumentVersions(documentId: string) {
  // Happy Path: Return list of versions for the protocol
  // Validation: Ensure documentId is valid UUID
  // Error State: Return empty array or throw 404 if no versions found
  // Empty State: Return empty list if no versions exist
  
  const response = await fetch(`/api/documents/${documentId}/versions`);
  
  if (!response.ok) {
    throw new Error("Failed to fetch versions");
  }
  
  return await response.json();
}
// Notes covered: call GET api/documents/{id}/versions get all the version for the specific document id.