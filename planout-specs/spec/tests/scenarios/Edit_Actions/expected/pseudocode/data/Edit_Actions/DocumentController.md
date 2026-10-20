/**
 * API Endpoints for the Edit Action Bar
 */

// GET /api/documents/:id
ROUTE GET "/api/documents/:id" (req, res) {
    const document = getDocument(req.params.id);
    res.status(200).json(document);
}

// PATCH /api/documents/:id/sections/:sectionId
ROUTE PATCH "/api/documents/:id/sections/:sectionId" (req, res) {
    const updatedSection = updateSectionContent(req.params.id, req.params.sectionId, req.body.content);
    res.status(200).json(updatedSection);
}

// DELETE /api/documents/:id/sections/:sectionId
ROUTE DELETE "/api/documents/:id/sections/:sectionId" (req, res) {
    const success = deleteSection(req.params.id, req.params.sectionId);
    res.status(204).send();
}