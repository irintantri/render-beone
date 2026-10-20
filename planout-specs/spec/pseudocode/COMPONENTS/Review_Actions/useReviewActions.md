// Custom hook to encapsulate business logic for the Review Page
HOOK useReviewActions(documentId) {
    STATE versions = []
    STATE loading = TRUE

    FUNCTION loadVersions() {
        versions = VersionService.fetchDocumentVersions(documentId)
        loading = FALSE
    }

    RETURN {
        versions,
        loading,
        compareVersions: VersionService.openSideBySide
    }
}