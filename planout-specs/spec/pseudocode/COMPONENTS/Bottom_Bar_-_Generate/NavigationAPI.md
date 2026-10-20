/**
 * API Signature Definition
 * Description: Defines the expected navigation paths for the Generate flow.
 */

INTERFACE NavigationRoutes {
    // Navigates user back to the initial configuration page
    BACK_TO_SETUP: "/create";
    
    // Navigates user to the editor, requiring a specific jobId
    SKIP_TO_EDIT: (jobId: string) => `/edit/${jobId}`;
}