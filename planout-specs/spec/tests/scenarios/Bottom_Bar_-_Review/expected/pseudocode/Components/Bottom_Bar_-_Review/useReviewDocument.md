// Custom hook to manage state and API interaction
HOOK useReviewDocument(documentId: string)
    STATE openCommentsCount = 0
    STATE isSubmitting = FALSE

    // Fetch initial state on mount
    ON_MOUNT
        RESPONSE = CALL GET /api/documents/{documentId}/status
        SET openCommentsCount = RESPONSE.openComments
    END ON_MOUNT

    FUNCTION submitDocumentForApproval(documentId)
        SET isSubmitting = TRUE
        TRY
            CALL POST /api/documents/{documentId}/submit-approval
            NAVIGATE_TO("/success-page")
        CATCH
            SHOW_ERROR("Failed to submit document")
        FINALLY
            SET isSubmitting = FALSE
        END TRY
    END FUNCTION

    RETURN { openCommentsCount, isSubmitting, submitDocumentForApproval }
END HOOK