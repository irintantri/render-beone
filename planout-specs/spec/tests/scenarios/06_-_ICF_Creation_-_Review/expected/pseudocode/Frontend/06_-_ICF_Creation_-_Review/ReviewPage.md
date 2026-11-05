// Node: Review Actions (b9070d07-9eed-4aa5-8c7c-c8a883f642f9)
// Description: Edit bar for Review page, includes version comparison.
// Happy Path: Displays version selector and diff toggle.
// Notes covered: Edit bar used in Review page, covering the compare versions.

// Node: Comment Actions (f66c79f2-7ad3-4b08-9bdf-8363e2efcbbc)
// Description: Comments tab on the right panel.
// Happy Path: Renders list of existing comments and input for new comments.
// Notes covered: Comments tab on the right panel of Review page.

// Node: Progress Stepper (fdc0a735-3711-4577-a5fe-f7ad2ce006d4)
// Description: Visual indicator of creation progress.
// Happy Path: Highlights current step in the ICF creation workflow.
// Notes covered: Progress stepper on each of the creation step.

// Node: Audit Trail (9498a524-52be-4d8d-b8ab-45f22ac5faec)
// Description: Chronological feed of document actions.
// API Call: GET /api/documents/:id/audit
// Happy Path: Maps response to list items. AI events (violet avatar), Human events (deterministic color).
// Fields: id, userId, action, timestamp, resourceId.
// Notes covered: Audit Trail tab, chronological feed, five data sources, colored avatars, title, action badge, actor name, timestamp.

// Node: Global Navigation Header (c194cc04-5b24-49b6-b418-b4d7885c1bb5)
// Description: Platform header.
// Happy Path: Displays platform title and user profile component.
// Notes covered: Global navigation header with platform title and user profile.

// Node: Bottom Bar - Review (0886ec86-5bc0-4bd5-ad93-2135e7ee8ab7)
// Description: Persistent footer for review actions.
// Happy Path: Contains primary action buttons (e.g., Approve, Reject).
// Notes covered: Bottom Bar - Review.

// Node: Wrapper Shell (5eb8b67c-f2e5-4a36-83d5-58b515df0616)
// Description: Layout container.
// Happy Path: Renders breadcrumbs, protocol name, and protocol ID.
// ORPHAN_FIELD: protocol_name
// ORPHAN_FIELD: protocol_id
// Notes covered: Wrapper consisting of breadcrumbs, protocol name and ID, etc.

// Node: Table of Contents (26743983-514c-4f77-8c0b-a4e7b046d7bb)
// Description: Left panel navigation.
// Happy Path: Renders hierarchical list of document sections.
// Notes covered: Generated document's Table of Contents on the left panel.