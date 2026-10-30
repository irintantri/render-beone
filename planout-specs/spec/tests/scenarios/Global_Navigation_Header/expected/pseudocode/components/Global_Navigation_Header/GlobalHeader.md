/**
 * Node: Left Section (3a69baa4-a561-4887-8160-5a5f767deb8f)
 * Asset: assets/77a95ca6-b9a9-49c8-8e20-8869ff95586e.svg
 */
Component LeftSection() {
    Render:
        - Attribution: "Powered by Agilisium"
        - Brand: "Consent IQ"
        - Subtitle: "Informed Consent Form Generation Platform"
    Notes covered: "Powered by Agilisium" attribution label, application brand name ("Consent IQ"), subtitle ("Informed Consent Form Generation Platform").
}

/**
 * Node: Functionality (cbe951b9-ec5e-48d2-84ec-956904a0f796)
 */
Component GlobalHeaderContainer() {
    Style: Position = Fixed, Width = 100%, Z-Index = High
    Render:
        <LeftSection />
        <NotificationIcon />
        <UserIdentity />
    Notes covered: Fixed header bar shown on every page.
}

/**
 * Node: Notification Icon (e5da0b21-d8d3-462f-bdfb-98225748a13c)
 */
Component NotificationIcon() {
    State: count = useUserContext().taskCounts.notifications
    Render:
        - Icon: Bell
        - Badge: Display count if count > 0
    Notes covered: Notification bell icon with unread badge count.
}

/**
 * Node: GET /api/user/context (fa28d791-86d4-4b34-b996-ee506b533bf9)
 */
Component UserIdentity() {
    Data: user = useUserContext() // Interface: { name, roles, avatar, taskCounts }
    
    Render:
        - Avatar: Initials-based (derived from user.firstName/lastName)
        - Name: user.firstName + user.lastName || "User Name"
        - Role: user.role || "ICF Author"
        - Icon: Dropdown chevron
    
    Happy Path: Data loaded, display user details.
    Empty State: Fallback to "User Name" and "ICF Author".
    Validation: If user object is null, trigger fallback strings.
    Notes covered: GET /api/user/context and load user identity (name, roles, avatar, task counts) from UserContext data table. User avatar (initials-based). Full name (Falls back to "User Name"). Role (Falls back to "ICF Author"). Dropdown chevron icon.
}