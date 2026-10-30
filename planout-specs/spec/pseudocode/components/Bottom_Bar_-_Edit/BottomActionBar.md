/**
 * Component: BottomActionBar
 * Asset: assets/654ba2f3-e0f3-4925-a8d3-d0cb06fad61f.svg
 */
Component BottomActionBar(props: { documentId: string, protocolId: string }) {
    
    // Node: Submit for Review (4523166b-31da-487f-b5bc-48f7062ac359)
    // Requirements: Display button, POST to API, navigate on success.
    Function handleSubmitForReview() {
        Try {
            // Cross-lane seam: Call logic layer
            Response = Logic.submitDocumentForReview(props.documentId);
            
            If (Response.status == 200) {
                // Transition: /review/{documentId}
                NavigateTo(`/review/${props.documentId}`);
            }
        } Catch (error) {
            DisplayErrorMessage("Failed to submit document for review.");
        }
    }

    // Node: Back to Setup (a9dff811-9b5e-4aa4-9e07-9799a76761ae)
    // Requirements: Display ghost button, navigate to setup.
    Function handleBackToSetup() {
        // Transition: /setup/{protocol_id}
        NavigateTo(`/setup/${props.protocolId}`);
    }

    Render {
        Container(className="bottom-action-bar") {
            Button(variant="ghost", onClick=handleBackToSetup) { "Back to Setup" }
            Button(variant="primary", onClick=handleSubmitForReview) { "Submit for Review" }
        }
    }
}

// Notes covered: 
// 1. Display Submit for Review button. 
// 2. If clicked then sends POST /api/documents/{documentId}/submit-review. 
// 3. Navigates to /review/{documentId}. 
// 4. Transitions the document status from Draft to In Review. 
// 5. Display "Back to Setup" ghost button. 
// 6. If clicked then navigates to /setup/{protocol_id}.