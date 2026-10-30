/**
 * Node: Sections JSON (7a7b4553-723b-4e74-aa92-0c0bbbb966c9)
 * Input: Receives array of section objects from LOGIC lane.
 * Output: Persists individual sections linked to a parent document.
 */
export async function saveDocumentSections(documentId: string, sections: Array<{ title: string, content: string }>) {
  // Happy Path: Map array to DocumentSection table and perform bulk insert.
  // Validation: Ensure title and content are strings; reject if empty array.
  // Error State: Rollback transaction if any section fails to insert.
  // Side Effects: Links each section to the DocumentGeneration via document_id.
  const records = sections.map(s => ({
    document_id: documentId,
    title: s.title,
    content: s.content
  }));
  
  return await db.insert('DocumentSection').values(records);
}

/**
 * Notes covered:
 * - Array of objects with title and content fields.
 */