COMPONENT ReviewBottomBar(documentId: string)
    // Hook to fetch document state and comment count
    DATA { openCommentsCount, isSubmitting } = useReviewDocument(documentId)
    
    // Navigation handler
    FUNCTION handleBackToEdit()
        NAVIGATE_TO("/edit-page")
    END FUNCTION

    // Submission handler
    FUNCTION handleSubmit()
        CALL submitDocumentForApproval(documentId)
    END FUNCTION

    // UI Layout based on Asset: assets/51f28719-6e79-4309-8c86-767cbbd45bf3.svg
    RENDER
        CONTAINER (BottomBar)
            BUTTON (BackToEdit, onClick: handleBackToEdit)
                LABEL: "Back to Edit"
            
            BUTTON (SubmitApproval, onClick: handleSubmit, disabled: isSubmitting)
                IF openCommentsCount > 0
                    LABEL: "Submit for Approval ({openCommentsCount} open)"
                ELSE
                    LABEL: "Submit for Approval"
                END IF
        END CONTAINER
    END RENDER
END COMPONENT