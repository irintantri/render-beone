// Custom hook to manage the state of the user and notifications
FUNCTION useUserContext():
    // State variables
    DEFINE userProfile AS { name, role, avatarInitials }
    DEFINE notificationCount AS INTEGER
    DEFINE isLoading AS BOOLEAN
    DEFINE error AS BOOLEAN

    // Fetch data from the backend
    FUNCTION fetchUserData():
        SET isLoading = TRUE
        TRY:
            RESPONSE = CALL GET "/api/user/context"
            SET userProfile = RESPONSE.data.user
            SET notificationCount = RESPONSE.data.unreadNotifications
        CATCH:
            SET error = TRUE
            // Fallbacks as per requirements
            SET userProfile = { name: "User Name", role: "ICF Author", avatarInitials: "UN" }
        FINALLY:
            SET isLoading = FALSE

    RETURN { userProfile, notificationCount, isLoading }