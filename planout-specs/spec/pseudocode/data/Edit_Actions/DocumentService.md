/**
 * Service to handle document and section lifecycle operations
 * triggered by the Edit Action Bar.
 */

// Fetch full document state for the Edit/Refine page
FUNCTION getDocument(documentId: UUID): Document {
    RETURN DB.Document.findUnique({ where: { id: documentId } });
}

// Persist manual text modifications to a specific section
FUNCTION updateSectionContent(documentId: UUID, sectionId: UUID, newContent: String): Section {
    // Update the section content
    const updatedSection = DB.Section.update({
        where: { id: sectionId, document_id: documentId },
        data: { content: newContent }
    });

    // Audit the manual edit
    DB.ActivityLog.create({
        data: {
            document_id: documentId,
            action_type: "MANUAL_EDIT",
            timestamp: CURRENT_TIMESTAMP
        }
    });

    RETURN updatedSection;
}

// Permanently remove a section and trigger re-sequencing
FUNCTION deleteSection(documentId: UUID, sectionId: UUID): Boolean {
    // Remove the section
    DB.Section.delete({
        where: { id: sectionId, document_id: documentId }
    });

    // Logic to re-sequence remaining sections to maintain document integrity
    const remainingSections = DB.Section.findMany({
        where: { document_id: documentId },
        orderBy: { sequence_order: "ASC" }
    });

    FOR EACH (index, section) IN remainingSections {
        DB.Section.update({
            where: { id: section.id },
            data: { sequence_order: index + 1 }
        });
    }

    RETURN TRUE;
}