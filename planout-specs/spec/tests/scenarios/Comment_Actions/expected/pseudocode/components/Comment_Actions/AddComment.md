/**
 * Node ID: 613e65a1-d9a0-412b-a12e-9e055dfa474c
 * Title: Add Comment
 * Description: At the bottom, a pinned composer lets the user add new comments. 
 * When focused, a custom section dropdown appears so the user can attach the comment to a specific section (defaults to whatever section is selected in the document). 
 * Clicking the submit button will submit the comment via `POST /api/comments`.
 */
Component AddComment(props: { selectedSectionId: string }) {
    State commentText = "";
    State targetSectionId = props.selectedSectionId;
    State isFocused = false;

    // Happy Path: User types comment, selects section, clicks submit.
    // Validation: Submit button disabled if commentText is empty.
    // Empty State: Placeholder "Write a comment..."
    // Side Effects: Triggers API call to Logic layer.

    Function handleSubmit() {
        // Cross-lane seam: Call Logic layer
        // Interface: POST /api/comments
        // Request: { content: commentText, sectionId: targetSectionId }
        // Response: { id: string, content: string, sectionId: string, timestamp: string }
        Logic.postComment({ 
            content: commentText, 
            sectionId: targetSectionId 
        }).then(onSuccess).catch(onError);
    }

    return (
        <Composer pinned>
            <Input 
                onFocus={() => isFocused = true} 
                onChange={(e) => commentText = e.target.value} 
            />
            {isFocused && (
                <SectionDropdown 
                    defaultValue={props.selectedSectionId}
                    onSelect={(id) => targetSectionId = id} 
                />
            )}
            <Button onClick={handleSubmit} disabled={!commentText}>Submit</Button>
        </Composer>
    );
}

// Notes covered:
// - At the bottom, a pinned composer lets the user add new comments.
// - When focused, a custom section dropdown appears so the user can attach the comment to a specific section.
// - Defaults to whatever section is selected in the document.
// - Clicking the submit button will submit the comment via `POST /api/comments`.