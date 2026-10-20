/**
 * Fetches the hierarchical structure of a document for the Table of Contents.
 * The TOC requires the list of sections ordered by their position field.
 */
FUNCTION getDocumentSections(documentId: UUID): List<Section> {
    RETURN DB.Section.findMany({
        where: { document_id: documentId },
        orderBy: { position: "ASC" },
        select: {
            id: true,
            title: true,
            position: true
        }
    });
}

/**
 * Creates a new section or subsection.
 * The position is automatically calculated as the max(position) + 1 
 * for the given document to ensure correct ordering in the TOC.
 */
FUNCTION createSection(documentId: UUID, title: String): Section {
    currentMaxPosition = DB.Section.max("position", { where: { document_id: documentId } });
    
    RETURN DB.Section.create({
        data: {
            document_id: documentId,
            title: title,
            position: (currentMaxPosition ?? 0) + 1,
            status: "DRAFT",
            version: "1.0.0"
        }
    });
}