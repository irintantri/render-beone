/**
 * Edit bar for version comparison and review actions.
 */
export const ReviewActions = ({ documentId }) => {
  const handleApprove = () => { /* Logic to transition status */ };
  const handleReject = () => { /* Logic to transition status */ };

  return (
    <div className="edit-bar">
      <button onClick={handleCompareVersions}>Compare Versions</button>
      <button onClick={handleApprove}>Approve</button>
      <button onClick={handleReject}>Reject</button>
    </div>
  );
};

// ORPHAN_FIELD: is_ai_generated (in metadata)
// ORPHAN_FIELD: section.id
// ORPHAN_FIELD: section.title
// ORPHAN_FIELD: section.body