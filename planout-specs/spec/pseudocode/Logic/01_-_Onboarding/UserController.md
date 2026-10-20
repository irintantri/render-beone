/**
 * Controller to handle the initialization of the authenticated user session.
 */
function getUserProfile(request) {
    // Extract authenticated user ID from session/token
    const userId = request.auth.userId;

    // Fetch core user profile data
    const user = database.USER.findUnique({
        where: { id: userId }
    });

    if (!user) {
        throw new Error("User not found", 404);
    }

    // Fetch task metrics for the dashboard summary
    const activeTasks = database.TASK.findMany({
        where: { assigneeId: userId }
    });

    // Calculate task counts based on status
    const draftsInProgress = activeTasks.filter(t => t.status === 'DRAFT').length; <!-- MISSING_FIELD: TASK.status_enum_draft -->
    const itemsAwaitingReview = activeTasks.filter(t => t.status === 'PENDING_REVIEW').length; <!-- MISSING_FIELD: TASK.status_enum_pending -->

    return {
        id: user.id,
        firstName: user.firstName,
        lastName: user.lastName,
        avatarUrl: user.avatarUrl,
        role: user.role,
        secondaryRole: user.secondaryRole,
        locale: user.locale,
        timezone: user.timezone,
        taskSummary: {
            draftsInProgress: draftsInProgress,
            itemsAwaitingReview: itemsAwaitingReview
        }
    };
}