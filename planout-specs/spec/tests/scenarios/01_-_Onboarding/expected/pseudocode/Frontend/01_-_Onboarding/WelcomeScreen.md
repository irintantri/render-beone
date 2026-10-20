import { useUserContext } from './hooks/useUserContext';

/**
 * Component: WelcomeScreen
 * Asset: assets/98687370-bb9f-4b08-9e10-f395d22a580e.svg
 */
export const WelcomeScreen = () => {
  const { user, isLoading, error } = useUserContext();

  if (isLoading) {
    return (
      <div className="full-screen-spinner">
        <Spinner />
        <p>Signing you in…</p>
      </div>
    );
  }

  if (!user) return <ErrorState />;

  return (
    <div className="welcome-container">
      {/* Left Column: Illustration */}
      <aside className="illustration-column">
        <IllustrationAsset />
        <p className="stats-text">500+ Protocols | 99% Compliance | 3x Faster</p>
      </aside>

      {/* Right Column: User Profile */}
      <main className="profile-column">
        <Avatar initials={`${user.firstName[0]}${user.lastName[0]}`} src={user.avatarUrl} />
        
        <h1>Welcome back, {user.firstName}</h1>
        
        <div className="role-badges">
          <Badge color="lilac" icon="pencil">{user.role}</Badge>
          {user.secondaryRole && (
            <>
              <span>·</span>
              <Badge color="mint" icon="check">{user.secondaryRole}</Badge>
            </>
          )}
        </div>

        <div className="task-summary">
          <p>
            <strong>{draftsInProgress}</strong> drafts in progress <!-- ORPHAN_FIELD: draftsInProgress -->
            {" and "}
            <strong>{itemsAwaitingReview}</strong> items awaiting your review <!-- ORPHAN_FIELD: itemsAwaitingReview -->
          </p>
        </div>

        <p className="disclaimer">Role permissions are managed by your organization administrator.</p>

        <button onClick={() => navigate('/dashboard')}>
          Continue to Dashboard
        </button>
      </main>
    </div>
  );
};