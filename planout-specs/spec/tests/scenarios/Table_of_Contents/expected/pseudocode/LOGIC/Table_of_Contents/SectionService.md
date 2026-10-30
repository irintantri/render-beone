/**
 * Node: Add Section Button (9f4aed36-7d3c-4d60-809e-92b5e93b4989)
 * Logic: Triggered by UI interaction.
 * 1. Execute POST /api/documents/:documentId/sections with body { "title": "New Section" }.
 * 2. On success, receive the new Section object.
 * 3. Trigger UI event to auto-select and scroll to the new section ID.
 * Notes covered: "Add Section" button, Creates a new section via POST /api/documents/{documentId}/sections with title "New Section", After creation, auto-selects and scrolls to the new section.
 */
async function addSection(documentId: string) {
  const response = await fetch(`/api/documents/${documentId}/sections`, {
    method: 'POST',
    body: JSON.stringify({ title: "New Section" })
  });
  const newSection = await response.json();
  return newSection; // UI layer handles selection/scroll
}

/**
 * Node: GET /api/documents/:id/sections (98230d0c-7ae3-4099-a0ef-7653408211ac)
 * Logic: Triggered on page load.
 * 1. Execute GET /api/documents/:id/sections.
 * 2. Return list of Section entities containing id, document_id, title, ai_label, status, content, position, version.
 * Notes covered: On load of the page, calls GET /api/documents/:id/sections and load the actual consent-form text, Given the document id, it returns a data list of sections, each carrying its own id, the document_id it belongs to, a title, an ai_label showing whether AI wrote it, a status, the content itself, a position for ordering, and a version.
 */
async function getSections(documentId: string) {
  const response = await fetch(`/api/documents/${documentId}/sections`, {
    method: 'GET'
  });
  return await response.json();
}

/**
 * Node: Add Subsection (113e24b1-ee8e-4838-a604-5e50ae505513)
 * Logic: Triggered by UI interaction.
 * 1. Execute POST /api/documents/:documentId/sections with body { "title": "New Subsection" }.
 * 2. On success, receive the new Section object.
 * 3. Trigger UI event to auto-select and scroll to the new subsection ID.
 * Notes covered: "Add Subsection" button, Creates a new subsection via POST /api/documents/{documentId}/sections with title "New Subsection", After creation, auto-selects and scrolls to the new subsection.
 */
async function addSubsection(documentId: string) {
  const response = await fetch(`/api/documents/${documentId}/sections`, {
    method: 'POST',
    body: JSON.stringify({ title: "New Subsection" })
  });
  const newSubsection = await response.json();
  return newSubsection; // UI layer handles selection/scroll
}