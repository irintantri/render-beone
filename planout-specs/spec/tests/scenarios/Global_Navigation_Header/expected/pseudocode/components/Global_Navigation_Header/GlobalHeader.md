// Main component for the Global Navigation Header
COMPONENT GlobalHeader:
    Asset: assets/77a95ca6-b9a9-49c8-8e20-8869ff95586e.svg
    
    IMPORT { useUserContext } FROM "./useUserContext"
    
    // Initialize data
    DATA { userProfile, notificationCount } = useUserContext()

    RENDER:
        HEADER (Fixed Position):
            // Left Section
            DIV class="brand-section":
                TEXT "Powered by Agilisium"
                H1 "Consent IQ"
                SPAN "Informed Consent Form Generation Platform"

            // Right Section
            DIV class="user-actions":
                // Notification Icon
                DIV class="notification-wrapper":
                    ICON "bell"
                    IF notificationCount > 0:
                        BADGE notificationCount

                // User Profile Section
                DIV class="user-profile-dropdown":
                    // Avatar (Initials-based)
                    DIV class="avatar":
                        TEXT userProfile.avatarInitials
                    
                    // User Info
                    DIV class="user-details":
                        SPAN userProfile.name
                        SPAN userProfile.role
                    
                    // Dropdown trigger
                    ICON "chevron-down"