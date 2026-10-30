// Component: DocumentEditBar
// Asset: assets/116d52e2-ece5-423b-9cc7-f887580bde74.svg

Component DocumentEditBar(documentId, sectionId) {
    // State
    state isEditing = false;
    state showPreview = false;
    state showDeleteConfirm = false;

    // Node: Document Name (3237b20b-0529-4eb1-8b90-b0fe673b4dcc)
    // Receives: document metadata from Logic.fetchDocument(documentId)
    // Renders: Top context bar displaying document name and ICF ID.
    // Notes covered: Context bar at the top shows the document name/ICF ID.

    // Node: Selected Section Title (803fda66-d25e-47b6-b6ee-5384bdbba001)
    // Renders: Title of the currently selected section.
    // Logic: Updates dynamically when sectionId prop changes.
    // Notes covered: Show the selected section title. If user selects another section then it should be reflected.

    // Node: ICF Version (04c60fc9-38ee-4cd9-872c-c1b6dbdb3306)
    // Renders: Version label (e.g., "v1.0 Draft").
    // Notes covered: The version label shows the current document version at a glance, such as "v1.0 Draft", so users always know which iteration they are viewing.

    // Node: Preview Draft (1230c612-6920-4ecf-af0d-958b3173192c)
    // Action: onClick -> set showPreview = true
    // Notes covered: Clicking Preview Draft opens a full-document PDF preview modal, letting the user review the final layout before committing to any changes.

    // Node: Edit (73cc4f5a-2e0a-45c5-b125-992ff53cd752)
    // Action: onClick -> set isEditing = true
    // If isEditing:
    //   - Render Textarea for section content
    //   - Render "Save" button -> calls Logic.saveSection(sectionId, content) -> set isEditing = false
    //   - Render "Cancel" button -> set isEditing = false
    // Notes covered: Clicking Edit button will switch the selected section to textarea editing mode. When it is on editing mode, display "Save" button on the bottom side of textarea and if clicked then persists edits via PATCH /api/sections/{id}. Display Cancel button on the right side of the Save button which will close the edit mode and do not save the edits.

    // Node: Delete (0c5a3ee2-e7f3-4b63-8a17-383d5758642c)
    // Action: onClick -> set showDeleteConfirm = true
    // Notes covered: Clicking Delete button opens the DeleteConfirmationModal. Shows a fixed overlay title "Delete this section?", warning text, Cancel and Delete buttons. Delete button on the modal calls DELETE /api/sections/{id}, clears selection, and refetches sections.

    if (showPreview) {
        return <PreviewModal onClose={() => setshowPreview(false)} />
    }
}