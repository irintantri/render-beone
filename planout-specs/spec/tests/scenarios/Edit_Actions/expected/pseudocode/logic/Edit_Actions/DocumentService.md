/**
 * Fetches the full document details including metadata and sections.
 * Used for initial page load of the Edit and Refine page.
 */
FUNCTION getDocument(documentId):
    RETURN Document.find(id = documentId)

/**
 * Updates a specific section's content.
 * Triggers an audit log entry for the manual edit.
 */
FUNCTION updateSection(documentId, sectionId, newContent):
    // Update the section content
    Section.update(
        id = sectionId,
        content = newContent
    )
    
    // Update document last_modified timestamp
    Document.update(
        id = documentId,
        last_modified = CURRENT_TIMESTAMP
    )
    
    // Audit logging
    ActivityLog.create(
        document_id = documentId,
        action_type = "MANUAL_EDIT",
        timestamp = CURRENT_TIMESTAMP
    )

/**
 * Permanently removes a section and re-sequences remaining sections.
 */
FUNCTION deleteSection(documentId, sectionId):
    // Remove the section
    Section.delete(id = sectionId)
    
    // Re-sequence remaining sections to maintain order
    remainingSections = Section.findAll(document_id = documentId).orderBy(sequence_order)
    FOR index, section IN remainingSections:
        Section.update(
            id = section.id,
            sequence_order = index + 1
        )
    
    // Update document last_modified timestamp
    Document.update(
        id = documentId,
        last_modified = CURRENT_TIMESTAMP
    )

/**
 * Generates a unique ICF ID for new documents.
 */
FUNCTION generateIcfId():
    year = CURRENT_YEAR
    randomNum = RANDOM_NUMBER(100, 999)
    // Format: PROTO-2026-782-ICF
    RETURN "PROTO-" + year + "-" + randomNum + "-ICF"