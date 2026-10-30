/**
 * Component: WelcomeScreen
 * Description: Role-aware welcome screen for authenticated users.
 * Asset: assets/98687370-bb9f-4b08-9e10-f395d22a580e.svg
 */

import { useUserContext } from './hooks/useUserContext';

export const WelcomeScreen = () => {
  const { user, taskCounts, isLoading, error } = useUserContext();

  if (isLoading) {
    return <LoadingState />;
  }

  if (error) {
    return <ErrorMessage message="Failed to load profile." />;
  }

  return (
    <div className="layout-container">
      <div className="left-column">
        <ImageIllustration />
        <div className="stats-footer">
          500+ Protocols | 99% Compliance | 3x Faster
        </div>
      </div>

      <div className="right-column">
        <WelcomeHeader user={user} />
        <RoleBadges role={user.role} secondaryRole={user.secondaryRole} />
        <TaskSummary taskCounts={taskCounts} />
        <ContinueButton />
        <p>Role permissions are managed by your organization administrator.</p>
      </div>
    </div>
  );
};