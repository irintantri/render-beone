export const WelcomeHeader = ({ user }) => {
  const initials = `${user.firstName[0]}${user.lastName[0]}`;
  
  return (
    <header>
      <div className="avatar-circle">{initials}</div>
      <h1>Welcome back, {user.firstName}</h1>
    </header>
  );
};