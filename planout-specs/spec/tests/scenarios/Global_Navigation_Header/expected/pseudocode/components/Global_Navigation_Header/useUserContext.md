/**
 * Node: `UserContext` (7798724b-08a3-4855-a8b5-02331aadbf2d)
 * Interface for Data Layer
 */
Interface UserContextDTO {
    id: string,
    firstName: string,
    lastName: string,
    role: string,
    secondaryRole: string,
    taskCounts: number
}

Function useUserContext() {
    // Logic: Fetch from /api/user/context
    // Ambiguity Flag: "taskCounts" is listed in DTO but "unread badge count" is requested in UI; 
    // assuming taskCounts maps to the notification badge.
    
    Try:
        response = API.get("/api/user/context")
        return response.data as UserContextDTO
    Catch:
        return DefaultUserContext // { firstName: "User", lastName: "Name", role: "ICF Author", ... }
}
Notes covered: UserContext DTO fields (id, firstName, lastName, role, secondaryRole, taskCounts).