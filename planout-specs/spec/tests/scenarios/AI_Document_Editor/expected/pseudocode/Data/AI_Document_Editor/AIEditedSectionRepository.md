/**
 * Unit: AI Edited Section JSON Schema (fec3fce1-e325-48dd-9e20-33e97703db27)
 * 
 * Description: Defines the data structure for an AI-edited ICF document section.
 * Receives: "section JSON Schema" from Logic swimlane (POST /api/documents/:id/sections/:id/ai).
 * Hands to: N/A (Terminal node).
 */

// Interface definition based on the provided JSON Schema
interface AIEditedSection {
  id: string; // UUID
  document_id: string; // UUID
  title: string;
  ai_label: 'AI Generated' | 'AI Edited' | 'AI Revised' | 'Manual' | null;
  status: 'Draft' | 'AI Generated' | 'Needs Review' | 'Approved';
  content: string; // Markdown
  position: number; // >= 0
  version: number; // >= 1
}

/**
 * Logic:
 * 1. Happy Path: Receive validated JSON payload from Logic layer, map to AIEditedSection entity, 
 *    and persist/return the object.
 * 2. Validation/Error: Ensure all required fields (id, document_id, title, ai_label, status, 
 *    content, position, version) are present. Validate enums for ai_label and status. 
 *    Validate constraints (position >= 0, version >= 1).
 * 3. Empty States: ai_label can be null. All other fields are strictly required.
 * 4. Side Effects: None (Data layer definition node).
 */

// Notes covered:
// - Section UUID (id)
// - UUID of the parent ICF document (document_id)
// - Section heading (title)
// - Provenance tag (ai_label)
// - Workflow state (status)
// - Full revised section body in Markdown (content)
// - Zero-based index (position)
// - Revision counter (version)
// - Additional properties forbidden (additionalProperties: false)
// - Required fields list (id, document_id, title, ai_label, status, content, position, version)