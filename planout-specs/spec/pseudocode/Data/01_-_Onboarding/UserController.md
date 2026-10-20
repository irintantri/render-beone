/**
 * Controller handling the /users/me endpoint.
 * Orchestrates the retrieval of user profile data and aggregates 
 * task counts for the dashboard initialization.
 */
function getCurrentUserSession(request) {
    const userId = request.auth.userId;

    // Fetch core user profile
    const user = DB.USER.findUnique({ where: { id: userId } });
    
    if (!user) {
        throw new Error("401: Unauthorized");
    }

    // Aggregate task counts based on user assignment
    const taskCounts = {
        draftsInProgress: DB.TASK.count({ where: { assigneeId: userId, status: 'draft' } }),
        itemsAwaitingReview: DB.TASK.count({ where: { assigneeId: userId, status: 'pending_review' } }),
        rejectedItems: DB.TASK.count({ where: { assigneeId: userId, status: 'rejected' } }),
        approvedToPublish: DB.TASK.count({ where: { assigneeId: userId, status: 'approved' } })
    };

    // Construct response payload
    return {
        id: user.id,
        firstName: user.firstName,
        lastName: user.lastName,
        email: user.email,
        avatarUrl: user.avatarUrl,
        role: user.role,
        secondaryRole: user.secondaryRole,
        locale: user.locale,
        timezone: user.timezone,
        lastLoginAt: user.lastLoginAt,
        taskCounts: taskCounts
    };
}