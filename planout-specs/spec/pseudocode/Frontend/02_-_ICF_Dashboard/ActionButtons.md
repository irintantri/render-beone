export const ActionButtons = ({ status, id, icfId }) => {
  const navigate = (path) => { /* Navigation logic */ };

  return (
    <div className="actions">
      <button onClick={() => navigate(`/preview/${icfId}`)}>View</button>
      {status === 'Draft' || status === 'In Review' ? (
        <button onClick={() => navigate(`/edit/${id}`)}>Open</button>
      ) : status === 'Approved' ? (
        <button onClick={() => navigate(`/preview/${icfId}`)}>Open</button>
      ) : (
        <span>—</span>
      )}
    </div>
  );
};