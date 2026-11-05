// Node: 07 - ICF Creation - Preview (01e2b39a-7c2a-4f69-8680-1c4ea18abe07)
// Triggered by: Actions (af34c83a-1d0b-479e-89e0-289d4ea91a5f) via "/preview/{id} for approved documents"

Component ICFPreviewPage:
  Props:
    - id: uuid (from route parameter)
  
  State:
    - icfContent: Blob | string <!-- ORPHAN_FIELD: icfContent -->
    - isPublishing: boolean
  
  Effect:
    - On mount, fetch document content using {id}.
  
  Render:
    - Display ICF as a simulated PDF page.
    - "Publish" button: Triggers final version publication.
    - Validation: Ensure document status is "approved" before allowing publish action.
    - Error State: Display "Document not found" or "Access denied" if fetch fails.
    - Happy Path: Document renders -> User clicks "Publish" -> API call to finalize -> Redirect to Dashboard.

Notes covered:
- Display the ICF as a simulated PDF page.
- Publish the final version.
- Fetch document content using id.
- Validation for "approved" status.
- Error state for fetch failure.
- Happy path for publish action.