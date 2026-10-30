/**
 * Node: raw JSON openrouter (6cb44c76-a58f-4164-a6f3-cbed95d921a3)
 * Input: Receives processed generation result from LOGIC lane.
 * Output: Persists the full generation state to the database.
 */
export async function saveDocumentGeneration(data: {
  template_id: string;
  source_filename: string;
  model: string;
  values: Record<string, string>;
  filled_markdown: string;
  structure_path: string;
  content_path: string;
  pages: number;
}) {
  // Happy Path: Insert record into DocumentGeneration table.
  // Validation: Ensure all required fields from the schema are present.
  // Empty State: If values are empty, store as empty JSON object.
  // Side Effects: Generates a new UUID for the document record.
  return await db.insert('DocumentGeneration').values({
    ...data,
    created_at: new Date()
  });
}

/**
 * Notes covered:
 * - template_id, source_filename, model, values (study_title, protocol_number, etc.), 
 *   unfilled (ignored as per schema), filled_markdown, structure_path, content_path, pages.
 */