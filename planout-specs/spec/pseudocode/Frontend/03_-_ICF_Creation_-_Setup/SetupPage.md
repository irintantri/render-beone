// Wrapper Shell (node id: b6420399-fc9b-47e9-8611-4bd6319fe6a2)
// Asset: assets/dd46e12b-d629-4482-aabd-05f3d2b04e38.svg
// The main container component providing the layout grid for the ICF setup wizard.
// Notes covered: None (Structural container)

// Global Navigation Header (node id: 64ba75c2-3563-430f-a012-e28aca7f1b18)
// Renders the top-level application navigation.
// Notes covered: None

// Progress Stepper (node id: 0c6db427-9b5b-4233-ab08-05b62f089d46)
// Renders the wizard progress indicator.
// Notes covered: None

// Select Protocol (node id: 5db5f18f-3031-48fe-8081-78ea8907412f)
// Logic: Calls GET /api/catalog/protocols on mount.
// UI: Displays a list of protocol cards. Each card shows `protocolId`, `phase`, `protocolName`, `category`.
// Selection: Clicking a card sets `selectedProtocol` state and applies `.selected` CSS class.
// Loading: Displays spinner during fetch.
// Notes covered: Load Protocol cards, Protocol ID and Phase badge, Protocol name, Metadata row (category, drug code <!-- ORPHAN_FIELD: drug_code -->), Selection logic, Loading state.

// Search Protocol (node id: ffe67465-abce-4767-9dd9-d8ba013961a8)
// UI: Text input with search icon, placeholder "Search protocols…".
// Validation: Triggers search only if input length >= 3.
// Logic: Calls GET /protocol/search?q={input} (Logic swimlane).
// Filtering: Performs client-side filtering of the protocol list by `protocolName` or `protocolId` (case-insensitive).
// Notes covered: Text input with search icon, placeholder "Search protocols…", Client-side filtering, Trigger search on >= 3 chars.

// Reference Documents (node id: b12a3b21-6aab-4e2f-9f04-a1ed3794e7e3)
// UI: Two categories: "Investigation Brochure" and "Lab Manual".
// Controls: "Fetch DMS" (calls GET /api/reference) and "Upload" (calls POST /api/reference/{protocolId}/upload).
// Upload State: Button shows "Uploading…" (disabled) -> "Uploaded" (check icon).
// Attached File: Displays document icon, `file_name`, "Attached" badge, and "×" remove button.
// Validation: Page-level `ErrorBanner` for "Select a protocol first" or upload failures.
// Notes covered: Two fixed categories, Fetch DMS button, Upload button, Uploading state, Attached file tag, Remove button, Info note, Validation errors.

// Select Template (node id: 3ed16b31-d4f2-4f2d-9614-c5d00529b5ff)
// Logic: Calls GET /api/catalog/templates on mount.
// UI: Displays template cards with `name`, `description`, and `recommended` badge.
// Selection: Default selection is "standard". Clicking a card updates `selectedTemplate`.
// Notes covered: Display available templates, Default selection "standard", Template name, Recommended badge, Description text, Selection logic.

// Bottom Bar - Setup (node id: 9dc15b2d-0174-41e5-bdab-8d8a44c6a033)
// Persistent footer for the setup wizard.
// Notes covered: None