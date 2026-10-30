/**
 * Component: DocumentReviewBar
 * Asset: assets/f754b406-69db-48ed-afd2-6d63f1fa2aae.svg
 */

// Node: Document Name (id: 83bfef6b-3a03-48e5-9a72-53a289b9bf30)
// Input: Props { documentName: string, icfId: string }
// Output: Rendered text element in the top context bar
function DocumentNameDisplay(props) {
  return <div>{props.documentName} | {props.icfId}</div>;
}
// Notes covered: Context bar at the top shows the document name/ICF ID.

// Node: ICF Version (id: 88bc2934-5cdf-4cd1-9061-5a98e565b8fd)
// Input: Props { versionLabel: string }
// Output: Rendered label (e.g., "v1.0 Draft")
function ICFVersionDisplay(props) {
  return <span>{props.versionLabel}</span>;
}
// Notes covered: The version label shows the current document version at a glance, such as "v1.0 Draft", so users always know which iteration they are viewing.

// Node: Compare Versions (id: fb08dcdd-dae3-419c-bdf4-225cd0ae2f72)
// Input: Triggered by user click
// Output: Cross-lane call to Logic.fetchDocumentVersions(documentId)
function CompareVersionsDropdown(props) {
  const [isOpen, setIsOpen] = useState(false);
  const [versions, setVersions] = useState([]);

  async function handleOpenDropdown() {
    setIsOpen(true);
    // Cross-lane seam: Call Logic API
    const data = await API.fetchDocumentVersions(props.documentId);
    setVersions(data);
  }

  return (
    <button onClick={handleOpenDropdown}>Compare Versions</button>
    {isOpen && (
      <ul>
        {versions.map(v => (
          <li key={v.id} onClick={() => props.onCompare(v.id)}>
            {v.versionString} - {v.status} {v.isCurrent ? "(current)" : ""}
          </li>
        ))}
      </ul>
    )}
  );
}
// Notes covered: "Compare Versions" button opens a dropdown listing all ICF versions for the same protocol. Each row shows version string, status badge, and "current" label for the active version. Clicking a different version opens the document version side by side with the current version.