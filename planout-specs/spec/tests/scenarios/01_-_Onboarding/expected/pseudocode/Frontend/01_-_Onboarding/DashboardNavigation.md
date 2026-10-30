// Node: Continue to Dashboard Button (518bd261-ea02-4af3-b7ac-47d36d88a965)
// Description: Clicking "Continue to Dashboard" button navigates to Dashboard page.
// Asset: assets/98687370-bb9f-4b08-9e10-f395d22a580e.svg
export const ContinueToDashboardButton = () => {
  const handleNavigate = () => {
    // Transition: "Dashboard page."
    router.push('/dashboard');
  };

  return <button onClick={handleNavigate}>Continue to Dashboard</button>;
};
// Notes covered: Clicking "Continue to Dashboard" button navigates to Dashboard page.