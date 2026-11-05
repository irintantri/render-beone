// Node: 03 - Consent setup and source selection (7c78667e-d9a0-44bf-b0ae-1b9b9699362c)
// Triggered by: Page Header (eeb59781-3936-49f7-adfa-9876a9eef4af) via "navigates to Setup page."

Component ConsentSetupPage:
  State:
    - selectedSource: string | null
    - setupConfig: object <!-- ORPHAN_FIELD: setupConfig -->
  
  Render:
    - Display selection interface for consent source (e.g., Template, Existing ICF, Upload).
    - Validation: Immediate check that a source is selected before enabling "Continue" button.
    - Empty State: Prompt user to select a source to proceed.
    - Happy Path: User selects source -> State updates -> "Continue" button enabled.
    - Side Effects: Persist selection to local state for downstream ICF creation steps.

Notes covered:
- Navigates to Setup page.
- Selection interface for consent source.
- Immediate validation for source selection.
- Empty state prompt.
- Happy path state update.
- Persist selection to local state.