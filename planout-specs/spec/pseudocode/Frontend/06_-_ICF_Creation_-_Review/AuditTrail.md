/**
 * Displays the chronological feed of document events.
 */
export const AuditTrail = ({ logs }) => {
  return (
    <div className="audit-trail">
      {logs.map((log) => (
        <div key={log.id} className="audit-entry">
          <Avatar user_id={log.user_id} />
          <div className="entry-details">
            <span className="action-badge">{log.action}</span>
            <span className="timestamp">{new Date(log.timestamp).toLocaleString()}</span>
          </div>
        </div>
      ))}
    </div>
  );
};