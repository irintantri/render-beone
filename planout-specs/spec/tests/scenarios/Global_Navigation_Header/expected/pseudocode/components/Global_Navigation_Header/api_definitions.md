// API Signature for the backend integration
ENDPOINT: GET /api/user/context
RESPONSE_SCHEMA:
{
  "user": {
    "name": "String",
    "role": "String",
    "avatarInitials": "String"
  },
  "unreadNotifications": "Integer"
}
// Logic: If the database (UserContext table) is unreachable, 
// the controller should return a 200 OK with default fallback values 
// to ensure the UI remains functional.