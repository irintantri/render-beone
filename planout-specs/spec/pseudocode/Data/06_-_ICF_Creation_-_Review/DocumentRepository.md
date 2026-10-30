/**
 * Node: Document Data Schema (fc34f433-9d87-4c39-aaa9-7ed385203c93)
 * Defines the persistence structure for ICF documents.
 */
interface DocumentDTO {
  id: string;
  protocol_id: string;
  icf_name: string;
  icf_version: string;
  template: string | null;
  status: string;
  content: string | null;
  metadata: Record<string, any>;
  published_at: string | null;
  created_at: string;
  last_modified: string;
}

// Happy Path: Returns a valid DocumentDTO object matching the schema.
// Validation: Enforces strict property presence as defined in the schema.
// Empty State: Returns null if the document ID is not found.
// Side Effects: None.
// Notes covered: DocumentDTO structure, required fields, property types, additionalProperties: false.