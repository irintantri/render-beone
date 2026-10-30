// Node: Global Navigation Header (20441089-a0a1-4d35-bb3b-7a947b85e3fb)
// Description: Standard application header.
// Happy Path: Renders static navigation elements.
// Notes covered: None (Empty description).

// Node: Wrapper Shell (38e8dc80-7fee-4b55-a570-9b64d07eca2a)
// Description: Layout container for the generation process.
// Happy Path: Provides centered layout context for child components.
// Notes covered: None (Empty description).

// Node: Generation checklist (a6ab8931-053d-4500-bc5e-bf293fa58c1f)
// Description: Displays 6 sequential steps with dynamic states.
// Logic: 
//   - Map steps: 1: Parsing, 2: Loading, 3: Applying, 4: Generating, 5: Compliance, 6: Finalizing.
//   - State logic: 
//     - Done: index < currentStep OR progress === 100 -> Green check icon, "Done".
//     - Active: index === currentStep AND progress < 100 -> Animated spinner, "In progress…".
//     - Pending: index > currentStep -> No icon, no label.
// Notes covered: 
// - During generation process, display generation steps with state.
// - Step 1: Parsing protocol data.
// - Step 2: Loading reference documents.
// - Step 3: Applying regulatory templates.
// - Step 4: Generating consent sections.
// - Step 5: Running compliance checks.
// - Step 6: Finalizing document.
// - Done state: Green check icon, "Done" label.
// - Active state: Animated spinner, "In progress…" label.
// - Pending state: No icon, no label.

// Node: Bottom Bar - Generate (6ce0b63d-942b-4058-a646-d49bdb323f98)
// Description: Footer container for generation controls.
// Happy Path: Renders static footer area.
// Notes covered: None (Empty description).

// Node: Progress Stepper (5f9d582f-2720-4253-b1a4-5402599b271e)
// Description: Orchestrates the polling of generation status.
// Logic: 
//   - Poll GET /api/icf/generation/{jobId} every 2 seconds.
//   - On response: Update local state (progress, step_label).
//   - If progress === 100: Redirect to /editor/{document_id}.
// Notes covered: None (Empty description).

// Node: Generation Visualization (85b1c5e2-ce33-486c-a194-da5cba941769)
// Description: Visual feedback for the generation process.
// Asset: assets/0f440293-ce09-4cbb-8748-0f9854854032.svg
// Logic:
//   - Title: "Generating Consent Form"
//   - Subtitle: "Creating ICF for {protocolId}" <!-- ORPHAN_FIELD: protocolId -->
//   - ETA: Calculate `max(0, round((100 - progress) * 3))` seconds, format as MM:SS.
//   - Progress Bar: Width = {progress}%.
//   - Footer: "{progress}% complete — please do not close this window".
// Notes covered:
// - Title: "Generating Consent Form".
// - Subtitle: "Creating ICF for {protocolId}" (bold protocol name).
// - ETA display: Clock icon with countdown in MM:SS format.
// - ETA calculation: `max(0, round((100 - progress) * 3))` seconds.
// - Progress bar: Track with animated fill bar, width set to `{progress}%`.
// - Footer: "{progress}% complete — please do not close this window".