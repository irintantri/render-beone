/**
 * Node: GET /users/me (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
 * Purpose: Provides authenticated session context, user identity, roles, and task metrics.
 */
async function getUserSessionContext(request: Request): Promise<UserSessionResponse> {
  // 1. Authentication Check
  // Input: Authorization header (Bearer token) or session cookie.
  // Logic: Validate session. If missing or expired, return 401 Unauthorized.
  const session = await validateSession(request.headers.authorization);
  if (!session) {
    throw new Error("401: Session missing or expired");
  }

  // 2. Data Retrieval
  // Fetch user profile from USER entity and task counts from TASK_SUMMARY entity.
  const user = await db.USER.findUnique({ where: { id: session.userId } });
  const taskCounts = await db.TASK_SUMMARY.findUnique({ where: { userId: session.userId } });

  // 3. Response Construction
  // Map database entities to the required JSON schema.
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
    taskCounts: {
      draftsInProgress: taskCounts.draftsInProgress,
      itemsAwaitingReview: taskCounts.itemsAwaitingReview,
      rejectedItems: taskCounts.rejectedItems,
      approvedToPublish: taskCounts.approvedToPublish
    }
  };
}

/**
 * Interface Definitions:
 * - Input: Request (via Logic swimlane)
 * - Output: UserSessionResponse (to Logic swimlane)
 * - Side Effects: None (Read-only operation)
 * - Happy Path: Returns 200 OK with full user profile and task summary.
 * - Error State: Returns 401 if authentication fails.
 * - Empty State: Not applicable (User must exist to have a session).
 */

// Notes covered:
// - Returns authenticated user's session context (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Personalise UI on load (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Provides identity fields, role assignments, and summary of pending work items (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Bootstrap dashboard without additional round-trips (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Request: no body required (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Authentication via session cookie or Bearer token (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Returns HTTP 401 if session missing or expired (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - Response payload schema: id, firstName, lastName, email, avatarUrl, role, secondaryRole, locale, timezone, lastLoginAt, taskCounts (7311ce52-0e7a-4d42-944a-6fe6cf92adac)
// - taskCounts: draftsInProgress, itemsAwaitingReview, rejectedItems, approvedToPublish (7311ce52-0e7a-4d42-944a-6fe6cf92adac)