// Logic layer for handling document versioning and comparison
SERVICE VersionService {

    // API Signature: GET /api/documents/{documentId}/versions
    FUNCTION fetchDocumentVersions(documentId) {
        RETURN HTTP.GET("/documents/" + documentId + "/versions")
        // Expected Response: [{id, versionString, status, isCurrent}]
    }

    // Logic for triggering the side-by-side view
    FUNCTION openSideBySide(baseVersionId, targetVersionId) {
        IF baseVersionId == targetVersionId:
            RETURN // Do nothing if comparing same version
            
        // Update URL or Global State to trigger the split-screen view
        ROUTER.push("/review/" + baseVersionId + "/compare/" + targetVersionId)
    }
}