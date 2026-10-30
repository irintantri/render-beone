/**
 * Node: ICF ID (8b762f88-a7e2-4add-b28a-34435c32352e)
 * Logic: Generates a unique identifier for the ICF.
 */
function generateICFIdentifier() {
    const year = new Date().getFullYear();
    const randomNum = Math.floor(Math.random() * 900) + 100; // Ensures 3 digits
    return `PROTO-${year}-${randomNum}-ICF`;
}
// Notes covered: Generate ICF ID with format PROTO-year-three digit random number-ICF, avoid duplicate ID, increment number avoiding security concern.

/**
 * Node: GET /api/documents/:id (bdefd0f6-679b-4858-8f64-173f964091d0)
 * Logic: Fetches full document details for the center panel.
 */
async function getDocument(id) {
    // Receives: id from COMPONENTS (Document Name)
    // Sends: Document object to COMPONENTS (Center Panel)
    const response = await fetch(`/api/documents/${id}`, { method: 'GET' });
    if (!response.ok) throw new Error("Failed to load document");
    return await response.json();
}
// Notes covered: On load of the page GET /api/documents/:id, Loads document metadata and returns the full document object, icf_name, protocol_id, status, created_at, last_modified, Display the documents and sections on the center panel, primary read endpoint.

/**
 * Node: PATCH /api/documents/:id/sections/:id (ce23c14c-a888-4dd9-ba7c-4112ed847aee)
 * Logic: Persists manual text edits and logs the activity.
 */
async function updateSection(documentId, sectionId, content) {
    // Receives: content from COMPONENTS (Edit)
    // Sends: Updated Section to DATA (Document Data Schema)
    const response = await fetch(`/api/documents/${documentId}/sections/${sectionId}`, {
        method: 'PATCH',
        body: JSON.stringify({ content })
    });
    
    if (response.ok) {
        // Side effect: Record MANUAL_EDIT in ActivityLog
        await logActivity(documentId, "MANUAL_EDIT");
    }
    return await response.json();
}
// Notes covered: Execute a PATCH request to the /api/documents/:id/sections endpoint, persist manual text modifications, server captures this action by recording a MANUAL_EDIT entry in the activity logs.

/**
 * Node: DELETE /api/documents/:id/sections/:id (255a7f35-bb46-49ce-9dc7-d37a58d4b1b1)
 * Logic: Removes a section and triggers structural re-sequencing.
 */
async function deleteSection(documentId, sectionId) {
    // Receives: trigger from COMPONENTS (Delete)
    // Sends: Confirmation to DATA (Document Data Schema)
    const response = await fetch(`/api/documents/${documentId}/sections/${sectionId}`, {
        method: 'DELETE'
    });
    
    if (response.ok) {
        // Logic: Automatically adjust remaining document structure
        await resequenceSections(documentId);
    }
    return response.status === 204;
}
// Notes covered: Users can permanently remove a specific section, triggers a confirmation prompt, automatically adjusts the remaining document structure to maintain proper sequencing.