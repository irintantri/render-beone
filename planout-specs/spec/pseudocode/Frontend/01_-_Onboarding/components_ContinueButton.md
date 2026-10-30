export const ContinueButton = () => {
  const navigate = useNavigate();
  return (
    <button onClick={() => navigate('/dashboard')}>
      Continue to Dashboard
    </button>
  );
};

/**
 * Notes covered:
 * - Clicking "Continue to Dashboard" button navigates to Dashboard page.
 * - Display text "Role permissions are managed by your organization administrator."
 * - Full-screen centered spinner with "Signing you in…" label while user context loads.
 * - Retrieve the authenticated user's profile and session details.
 * - User should be able to see left column displaying the Image illustration.
 * - On below side, there are copy text stating 500+ Protocols | 99% Compliance | 3x Faster.
 * - Avatar - large circular avatar rendered from user initials.
 * - Welcome Title - "Welcome back, {firstName}".
 * - User Role - Primary role in lilac badge, secondaryRole in mint badge with "·" divider.
 * - Task Summary - Display task summary with bolded values.
 * - Call the profile API to get the details.
 */