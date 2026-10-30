/**
 * Node: User Input and Instruction Selection (d2010a32-ebe5-42d2-bc5b-fc55d4d92571)
 * Receives: 
 *   - prompt (string) from "Add instruction" (COMPONENTS)
 *   - section context (AIEditedSection) from "Ask AI Button" (COMPONENTS)
 * Logic:
 *   1. Combines the current section content and the user's prompt.
 *   2. Prepares the payload for the OpenRouter SDK integration.
 *   3. Triggers the POST /api/documents/:id/sections/:id/ai endpoint.
 * Notes covered:
 *   - The selected section and the user's prompt are combined and sent to the OpenRouter SDK.
 *   - Use the prompt as the instruction and the section as the context for precise, AI-powered revision.
 */

/**
 * Node: POST /api/documents/:id/sections/:id/ai (8e2f444b-e4af-4976-8c9d-7cee4160bd7f)
 * Receives: 
 *   - prompt and section_id from "User Input and Instruction Selection" (Logic)
 * Logic:
 *   1. Validates the request parameters.
 *   2. Calls the AI provider (OpenRouter) to generate the revised content.
 *   3. Maps the AI response to the AIEditedSection schema.
 *   4. Sets ai_label to 'AI Edited'.
 *   5. Sets status to 'AI Generated'.
 *   6. Increments the version field.
 *   7. Returns the updated AIEditedSection object.
 * Happy Path: Returns 200 OK with the updated AIEditedSection JSON.
 * Error State: Returns 400/500 if the AI provider is unreachable or returns invalid content.
 * Side Effects: Updates the database record for the specific section.
 * Notes covered:
 *   - This endpoint results from AI refine one section from a natural-language prompt.
 *   - Return the edited section JSON Schema.
 */