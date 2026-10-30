/**
 * Node: GET /users/me (f358e2c8-39b1-4889-8db4-5528738310fe)
 * Logic: Orchestrates the retrieval of user profile and associated task metrics.
 */
async function getUserProfile(req, res) {
    // 1. Authentication Check
    // Verify session via Authorization header or session cookie.
    // If missing or expired, return 401 Unauthorized.
    const userId = await authService.verifySession(req);
    if (!userId) {
        return res.status(401).json({ error: "Session missing or expired" });
    }

    // 2. Data Retrieval
    // Fetch primary user details from USER entity.
    const user = await db.USER.findUnique({ where: { id: userId } });
    
    // Fetch task summary from TASK_SUMMARY entity.
    const taskSummary = await db.TASK_SUMMARY.findUnique({ where: { userId: userId } });

    // 3. Response Construction
    // Map fields verbatim from USER and TASK_SUMMARY.
    const responsePayload = {
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
        taskCounts: {
            draftsInProgress: taskSummary.draftsInProgress,
            itemsAwaitingReview: taskSummary.itemsAwaitingReview,
            rejectedItems: taskSummary.rejectedItems,
            approvedToPublish: taskSummary.approvedToPublish
        }
    };

    return res.status(200).json(responsePayload);
}

/**
 * Notes covered:
 * - Retrieve authenticated user's profile and session details.
 * - Response includes identity information (display name, avatar, roles).
 * - Response includes dynamic data (task counts, regional settings).
 * - Interface is personalized and up to date.
 * - Authentication via session cookie or Bearer token.
 * - Returns HTTP 401 if session is missing or expired.
 * - Maps USER fields: id, firstName, lastName, email, avatarUrl, role, secondaryRole, locale, timezone, lastLoginAt.
 * - Maps TASK_SUMMARY fields: draftsInProgress, itemsAwaitingReview, rejectedItems, approvedToPublish.
 */