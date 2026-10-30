// Node: Notes (850832c9-c315-4ddd-b5c0-b5ce0e61735b)
// Description: Display text "Role permissions are managed by your organization administrator."
export const RolePermissionsNote = () => {
  return <p>Role permissions are managed by your organization administrator.</p>;
};
// Notes covered: Display text "Role permissions are managed by your organization administrator."

// Node: Loading state (f235e85b-4b4d-4656-89eb-650a40769bfa)
// Description: Full-screen centered spinner with "Signing you in…" label while user context loads.
export const LoadingState = () => {
  // Trigger: "user context loads." -> Logic swimlane GET /users/me
  return (
    <div className="full-screen-center">
      <Spinner />
      <p>Signing you in…</p>
    </div>
  );
};
// Notes covered: Full-screen centered spinner with "Signing you in…" label while user context loads.

// Node: Image Illustration (340b0624-100e-47e5-a995-634d3ecb113e)
// Description: Left column displaying the Image illustration related with AI-powered Informed Consent Form authoring platform.
// Description: Below side, copy text stating 500+ Protocols | 99% Compliance | 3x Faster.
export const ImageIllustration = () => {
  return (
    <aside>
      <img src="ai-compliance-illustration.png" alt="AI-powered ICF platform" />
      <footer>
        <span>500+ Protocols | 99% Compliance | 3x Faster</span>
      </footer>
    </aside>
  );
};
// Notes covered: User should be able to see left column displaying the Image illustration related with AI-powered Informed Consent Form authoring platform for clinical research compliance and efficiency; On below side, there are copy text stating 500+ Protocols | 99% Compliance | 3x Faster

// Node: Welcome Title (730f8a6e-051b-429b-be53-7def68f744cd)
// Description: Avatar, Welcome Title, User Role, Task Summary.
// Trigger: "Call the profile API" -> Logic swimlane GET /users/me
export const WelcomeHeader = ({ user, taskSummary }) => {
  const initials = `${user.firstName[0]}${user.lastName[0]}`;
  
  return (
    <header>
      <div className="avatar">{user.avatarUrl ? <img src={user.avatarUrl} /> : initials}</div>
      <h1>Welcome back, {user.firstName}</h1>
      
      <div className="roles">
        <span className="badge-lilac"><IconPencil /> {user.role}</span>
        {user.secondaryRole && (
          <>
            <span>·</span>
            <span className="badge-mint"><IconRelevant /> {user.secondaryRole}</span>
          </>
        )}
      </div>

      <div className="task-summary">
        <p>
          <strong>{taskSummary.draftsInProgress}</strong> drafts in progress | 
          <strong>{taskSummary.itemsAwaitingReview}</strong> items awaiting your review
        </p>
      </div>
    </header>
  );
};
// Notes covered: Avatar - large circular avatar rendered from user initials; Welcome Title - "Welcome back, {firstName}"; User Role - Primary role displayed in a lilac badge with pencil icon; If secondaryRole exists, a second mint-colored badge is shown with a relevant icon, separated by a "·" divider; Task Summary - Display task summary associated with the user profile; Fallback to sentence stating "{draftsInProgress} drafts in progress" and "{itemsAwaitingReview} items awaiting your review" - both values bolded; Call the profile API to get the details