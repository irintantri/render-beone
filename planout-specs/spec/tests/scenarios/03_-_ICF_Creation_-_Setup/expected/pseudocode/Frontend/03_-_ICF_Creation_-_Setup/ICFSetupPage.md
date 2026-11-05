// Wrapper Shell (node id: b6420399-fc9b-47e9-8611-4bd6319fe6a2)
// Asset: assets/dd46e12b-d629-4482-aabd-05f3d2b04e38.svg
// The main layout container providing the grid for the three-column wizard.
// Notes covered: None (Structural)

// Global Navigation Header (node id: 64ba75c2-3563-430f-a012-e28aca7f1b18)
// Renders the top-level application navigation.
// Notes covered: None (Structural)

// Progress Stepper (node id: 0c6db427-9b5b-4233-ab08-05b62f089d46)
// Displays the current step in the ICF creation process.
// Notes covered: None (Structural)

// Select Protocol (node id: 5db5f18f-3031-48fe-8081-78ea8907412f)
// State: `selectedProtocol` (object), `isLoading` (boolean).
// On mount: Call GET /api/catalog/protocols.
// Render: List of cards. Each card displays `protocolId`, `phase`, `protocolName`, `category`.
// Interaction: Click card -> set `selectedProtocol`. Apply `.selected` CSS class.
// Notes covered: Load Protocol cards, Protocol ID and Phase badge, Protocol name, Metadata row (category, drug code <!-- ORPHAN_FIELD: drug_code -->), Selection logic, Loading state.

// Search Protocol (node id: ffe67465-abce-4767-9dd9-d8ba013961a8)
// Input: Text field, placeholder "Search protocols…".
// Validation: Trigger GET /protocol/search?q={value} only if value.length >= 3.
// Logic: Client-side filtering of the protocol list by `protocolName` or `protocolId` (case-insensitive).
// Notes covered: Text input with search icon, placeholder "Search protocols…", Client-side filtering, Trigger search on >= 3 chars.

// Reference Documents (node id: b12a3b21-6aab-4e2f-9f04-a1ed3794e7e3)
// State: `attachedFiles` (Map of `doc_kind` to file metadata).
// Render: Two categories: "Investigation Brochure" and "Lab Manual".
// Controls: "Fetch DMS" (calls GET /api/reference?protocolId={selectedProtocol.protocolId}) and "Upload" (hidden file input).
// Upload: `accept=".pdf,.doc,.docx,.txt,.md"`. On change, POST /api/reference/{protocolId}/upload.
// UI: While uploading, button = "Uploading…" (disabled). Success = check icon + "Uploaded".
// Tag: Display file name (tooltip), "Attached" badge, "×" remove button.
// Validation: If "Fetch DMS" or "Upload" clicked without `selectedProtocol`, show ErrorBanner "Select a protocol first".
// Notes covered: Two fixed categories, Fetch DMS button, Upload button, Upload state, Attached file tag, Remove logic, Info note, Validation errors.

// Select Template (node id: 3ed16b31-d4f2-4f2d-9614-c5d00529b5ff)
// State: `selectedTemplate` (default: "standard").
// On mount: Call GET /api/catalog/templates.
// Render: Cards with `name`, `description`, `recommended` badge.
// Interaction: Click card -> set `selectedTemplate` to `id`.
// Notes covered: Display available templates, Default selection "standard", Template name, Recommended badge, Description text, Selection logic.

// Bottom Bar - Setup (node id: 9dc15b2d-0174-41e5-bdab-8d8a44c6a033)
// Contains primary action buttons for the wizard.
// Notes covered: None (Structural)