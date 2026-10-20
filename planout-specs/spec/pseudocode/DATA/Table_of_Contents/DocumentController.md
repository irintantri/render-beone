/**
 * API Endpoint: GET /api/documents/:id/sections
 * Returns the ordered list of sections used to render the Table of Contents.
 */
ENDPOINT GET /api/documents/:id/sections(id: UUID) {
    sections = DocumentRepository.getDocumentSections(id);
    RETURN HTTP 200 OK (sections);
}

/**
 * API Endpoint: POST /api/documents/:id/sections
 * Used by "Add Section" and "Add Subsection" buttons.
 */
ENDPOINT POST /api/documents/:id/sections(id: UUID, body: { title: String }) {
    newSection = DocumentRepository.createSection(id, body.title);
    RETURN HTTP 201 CREATED (newSection);
}