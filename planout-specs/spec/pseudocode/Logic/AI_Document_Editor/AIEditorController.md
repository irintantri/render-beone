/**
 * Handles the AI refinement process for a specific document section.
 */
async function handleAIRefinement(documentId: UUID, sectionId: UUID, userPrompt: string) {
  // 1. Fetch the current section state to provide context to the AI
  const currentSection = await database.AIEditedSection.findUnique({
    where: { id: sectionId, document_id: documentId }
  });

  if (!currentSection) {
    throw new Error("Section not found");
  }

  // 2. Prepare context for the OpenRouter SDK
  // We combine the existing content with the user's specific instruction
  const aiContext = {
    originalContent: currentSection.content,
    instruction: userPrompt,
    title: currentSection.title
  };

  // 3. Invoke AI Service (OpenRouter SDK)
  // The service processes the prompt and returns the refined content
  const refinedContent = await OpenRouterService.generateRefinement(aiContext);

  // 4. Update the section in the database
  // Increment version to maintain audit trail of edits
  const updatedSection = await database.AIEditedSection.update({
    where: { id: sectionId },
    data: {
      content: refinedContent,
      version: currentSection.version + 1,
      status: "refined"
    }
  });

  return updatedSection;
}