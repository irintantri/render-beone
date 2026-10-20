/**
 * Component: BottomActionBar
 * Purpose: Provides navigation and action triggers for the Edit and Refine page.
 * Asset: assets/bottom-bar-edit.svg
 */

Component BottomActionBar(documentId, protocolId) {
    // State management for loading status during API calls
    State isSubmitting = false;

    // Handler for "Back to Setup"
    Function handleBackToSetup() {
        NavigateTo("/setup/" + protocolId);
    }

    // Handler for "Submit for Review"
    Async Function handleSubmitForReview() {
        Set isSubmitting = true;
        
        Try {
            // Call the logic service
            Response = await DocumentService.submitForReview(documentId);
            
            If (Response.success) {
                NavigateTo("/review/" + documentId);
            }
        } Catch (error) {
            ShowToast("Failed to submit document: " + error.message);
        } Finally {
            Set isSubmitting = false;
        }
    }

    Render {
        Container(style: "bottom-bar-layout") {
            // Ghost button for navigation
            Button(
                label: "Back to Setup",
                variant: "ghost",
                onClick: handleBackToSetup
            );

            // Primary action button
            Button(
                label: "Submit for Review",
                variant: "primary",
                disabled: isSubmitting,
                onClick: handleSubmitForReview
            );
        }
    }
}