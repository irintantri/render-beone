/**
 * API Route definition for AI Document Editor
 */
router.post("/api/documents/:id/sections/:id/ai", async (req, res) => {
  const { id: documentId, sectionId } = req.params;
  const { prompt } = req.body;

  try {
    const result = await handleAIRefinement(documentId, sectionId, prompt);
    res.status(200).json(result);
  } catch (error) {
    res.status(500).json({ error: "Failed to refine section with AI" });
  }
});