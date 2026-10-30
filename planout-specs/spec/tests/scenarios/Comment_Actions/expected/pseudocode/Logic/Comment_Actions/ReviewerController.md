// Node: POST /api/reviewers/{id}/act (c0e7259c-f73b-4658-bf6f-c42b547d2373)
// Input: Triggered by "Act" button click from Approval Gate (components).
// Logic:
FUNCTION handleReviewerAct(id):
    TRY:
        UPDATE Reviewer SET acted = true WHERE id = id
        RETURN 200 OK
    CATCH:
        RETURN error to caller for upstream handling
// Output: Updates Reviewer entity in Data layer.
// Notes covered: Request dispatched with reviewer's id as path parameter; On success, reviewer's status updated to "acted"; If request fails, error surfaced to caller.