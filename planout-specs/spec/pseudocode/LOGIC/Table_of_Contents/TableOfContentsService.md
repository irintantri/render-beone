/**
 * Fetches all sections for a specific document to populate the Table of Contents.
 * @param {string} documentId - The UUID of the document.
 */
FUNCTION fetchDocumentSections(documentId):
    // Call GET /api/documents/:id/sections
    // Map response to a sorted list based on Section.position
    RETURN sortedSections

/**
 * Creates a new section or subsection.
 * @param {string} documentId - The UUID of the document.
 * @param {string} title - The title for the new section.
 */
FUNCTION createSection(documentId, title):
    // Call POST /api/documents/:id/sections
    // Payload: { "title": title, "document_id": documentId }
    // Return the created Section object
    RETURN newSection