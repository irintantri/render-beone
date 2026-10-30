/**
 * Component: BottomBarGenerate
 * Asset: assets/d4357674-d49a-4826-8fbb-8813a446b9c2.svg
 */
Component BottomBarGenerate(props: { jobId: string }) {
    
    // Node: Back to Setup (id: a8c211fb-50f3-4174-bef6-9f0854855aff)
    // Description: "Back to Setup" ghost button → navigates to `/create`.
    UI_Element GhostButton_BackToSetup {
        Label: "Back to Setup"
        OnClick: () => {
            NavigateTo("/create")
        }
    }

    // Node: Skip Button (id: 85ede8de-913b-42b9-aab6-845dd97ab66e)
    // Description: "Skip" ghost button → navigates to `/edit/{jobId}` (allows jumping ahead before completion).
    UI_Element GhostButton_Skip {
        Label: "Skip"
        OnClick: () => {
            // Ambiguity: If jobId is null/undefined, navigation path is invalid. 
            // Resolution: Ensure jobId is validated as present before triggering navigation.
            If (props.jobId exists) {
                NavigateTo("/edit/" + props.jobId)
            } Else {
                Log_Error("Missing jobId for skip navigation")
            }
        }
    }

    Render {
        Container(style: "Bottom-bar-generate-layout") {
            GhostButton_BackToSetup()
            GhostButton_Skip()
        }
    }
}

/* 
Notes covered:
- "Back to Setup" ghost button (a8c211fb-50f3-4174-bef6-9f0854855aff)
- navigates to `/create` (a8c211fb-50f3-4174-bef6-9f0854855aff)
- "Skip" ghost button (85ede8de-913b-42b9-aab6-845dd97ab66e)
- navigates to `/edit/{jobId}` (85ede8de-913b-42b9-aab6-845dd97ab66e)
- allows jumping ahead before completion (85ede8de-913b-42b9-aab6-845dd97ab66e)
*/