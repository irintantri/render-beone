COMPONENT ReviewActionBar(documentId, currentVersionId)
    // State management for the version dropdown
    STATE isDropdownOpen = FALSE
    STATE availableVersions = []
    
    // Fetch versions on mount
    EFFECT ON MOUNT:
        availableVersions = API.fetchDocumentVersions(documentId)

    RENDER:
        Container(class="review-action-bar") {
            // Contextual Info
            Text(documentName) // From documentId context
            Badge(currentVersionLabel) // e.g., "v1.0 Draft"
            
            // Asset: assets/f754b406-69db-48ed-afd2-6d63f1fa2aae.svg
            Button("Compare Versions", onClick: toggleDropdown)
            
            IF isDropdownOpen:
                VersionDropdown(
                    versions: availableVersions,
                    onSelect: (selectedVersion) => {
                        TRIGGER CompareService.openSideBySide(currentVersionId, selectedVersion.id)
                        isDropdownOpen = FALSE
                    }
                )
        }