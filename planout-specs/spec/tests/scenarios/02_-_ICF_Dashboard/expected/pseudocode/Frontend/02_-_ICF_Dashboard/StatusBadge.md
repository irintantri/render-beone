export const StatusBadge = ({ status }) => (
  <span className={`badge-${status.toLowerCase().replace(' ', '-')}`}>
    {status}
  </span>
);