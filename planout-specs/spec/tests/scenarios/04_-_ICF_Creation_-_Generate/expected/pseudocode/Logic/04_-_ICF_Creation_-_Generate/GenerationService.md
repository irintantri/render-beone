/**
 * Node: Fetch on load (cb92b100-711d-4cfb-bef5-6fd82c078523)
 * 
 * Logic:
 * 1. On component mount, initialize an EventSource connection to GET /api/icf/generation/{jobId}.
 * 2. Listen for incoming events:
 *    - Update local state with 'progress' (percentage) and 'step_label'.
 *    - Highlight the current step in the UI based on 'step_label'.
 * 3. Handle 'status' updates:
 *    - If status is "complete":
 *      a. Close the SSE connection.
 *      b. Trigger a 700ms timer.
 *      c. After timer, navigate to "/edit/{document_id}".
 * 
 * Happy Path: SSE stream provides incremental updates, completes, and redirects.
 * Error State: If connection fails, log error and display a retry prompt to the user.
 * Empty State: Initial state shows 0% progress and first step highlighted.
 * Side Effects: SSE connection lifecycle management, browser navigation.
 * 
 * Notes covered:
 * - On mount, the component opens an SSE connection to GET /api/icf/generation/{jobId}.
 * - Each event carries status, progress percentage, step label, and optionally a document_id.
 * - Component updates progress bar and highlights current step.
 * - When server sends status: "complete" with a document_id, SSE stream closes.
 * - Auto-navigates to /edit/{documentId} after a 700ms delay.
 */