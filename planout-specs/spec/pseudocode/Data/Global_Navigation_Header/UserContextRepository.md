/**
 * Node: `UserContext` (ID: 7798724b-08a3-4855-a8b5-02331aadbf2d)
 * Description: Data access layer for retrieving user identity and profile metadata.
 */

// Interface definition for the DTO
interface UserContextDTO {
  id: string;
  firstName: string;
  lastName: string;
  role: string;
  secondaryRole: string;
  taskCounts: number;
}

/**
 * Logic: Handles the retrieval of user identity from the UserContext data table.
 * Input: Triggered by GET /api/user/context (Cross-lane seam from Logic/Components)
 * Output: Returns UserContextDTO to the Logic layer.
 */
async function getUserContext(userId: string): Promise<UserContextDTO> {
  // Happy Path: Query the UserContext table by ID
  const user = await db.UserContext.findUnique({
    where: { id: userId }
  });

  if (!user) {
    // Error/Empty State: Return default values if user data is unavailable
    // Note: The requirement specifies fallbacks for name and role in the UI layer.
    // We provide a structured object to ensure the UI can handle these defaults.
    return {
      id: userId,
      firstName: "User",
      lastName: "Name",
      role: "ICF Author",
      secondaryRole: "",
      taskCounts: 0
    };
  }

  return {
    id: user.id,
    firstName: user.firstName,
    lastName: user.lastName,
    role: user.role,
    secondaryRole: user.secondaryRole,
    taskCounts: user.taskCounts
  };
}

// Notes covered:
// - DTO definition: id, firstName, lastName, role, secondaryRole, taskCounts
// - GET /api/user/context triggers data load
// - Load user identity (name, roles, avatar, task counts) from UserContext data table
// - Fallback logic for name ("User Name") and role ("ICF Author") when data is unavailable