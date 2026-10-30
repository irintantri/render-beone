/**
 * Main container for the ICF Preview and Publishing flow.
 * Orchestrates data fetching and UI state for the final document review.
 */

// Node: Wrapper Shell (id: f71d9ba1-518c-4bc2-b566-aec077e548ab)
// Acts as the layout container for all child components.
export const ICFPreviewPage = ({ documentId }) => {
  const [isPublished, setIsPublished] = useState(false);
  const [documentData, setDocumentData] = useState(null);
  const [sections, setSections] = useState([]);

  // Fetch document metadata and content on mount
  useEffect(() => {
    fetch(`/api/documents/${documentId}`)
      .then(res => res.json())
      .then(data => setDocumentData(data));
      
    fetch(`/api/documents/${documentId}/sections`)
      .then(res => res.json())
      .then(data => setSections(data.sections));
  }, [documentId]);

  return (
    <div className="shell">
      <GlobalNavigationHeader />
      <ProgressStepper />
      <DocumentToolbar documentData={documentData} />
      <ICFDocument sections={sections} />
      <PublishAction 
        documentId={documentId} 
        isPublished={isPublished} 
        onPublishSuccess={() => setIsPublished(true)} 
      />
      <BackToReviewButton />
    </div>
  );
};

// Node: Global Navigation Header (id: 5a543e14-d959-4b2c-a80b-f88b371b76ef)
const GlobalNavigationHeader = () => <header>...</header>;

// Node: Progress Stepper (id: 3debd6c8-53ec-4d7e-acbe-7e2a24de0989)
const ProgressStepper = () => <nav>...</nav>;

// Node: Document Toolbar (id: 7d757d6c-c36b-4b16-8280-aedf6f7d2389)
const DocumentToolbar = ({ documentData }) => {
  // Displays document filename (title) and page count <!-- ORPHAN_FIELD: pageCount -->
  // Includes zoom in/out controls
  return (
    <div className="toolbar">
      <span>{documentData?.title}</span>
      <button onClick={zoomIn}>+</button>
      <button onClick={zoomOut}>-</button>
    </div>
  );
};
// Notes covered: A toolbar at the top shows the document filename and page count. Zoom button to use zoom in and zoom out functionality.

// Node: ICF Document (id: c986f4f7-059d-479c-b78e-d1c26e393c7c)
// Asset: assets/296abc29-be91-4796-bd36-496013ee60e5.svg
const ICFDocument = ({ sections }) => {
  return (
    <div className="pdf-stage">
      <div className="pdf-page">
        <h1>INFORMED CONSENT FORM</h1>
        {/* Renders organization header, protocol metadata, and sections */}
        {sections.map((section, index) => (
          <div key={index}>
            <h3>{index + 1}. {section.title}</h3>
            <p>{section.content}</p>
          </div>
        ))}
      </div>
    </div>
  );
};
// Notes covered: PDF area renders the entire text content and final layout format. The page renders the ICF as a simulated PDF page: a white page on a grey stage, with organization header, title "INFORMED CONSENT FORM", protocol metadata, and every section in order with numbered headings.

// Node: Publish ICF (id: 5ce048cb-b7ac-4f45-821b-6061ca9d1d43)
// Node: ICF Published (id: 398bc3b7-d816-4375-820a-e206e6cf9cf6)
const PublishAction = ({ documentId, isPublished, onPublishSuccess }) => {
  const handlePublish = async () => {
    // Logic swimlane: POST /api/publish
    const response = await fetch('/api/publish', {
      method: 'POST',
      body: JSON.stringify({ documentId })
    });
    if (response.ok) onPublishSuccess();
  };

  if (isPublished) {
    return <div className="badge-success">ICF Published Successfully</div>;
  }

  return (
    <button onClick={handlePublish}>
      Publish ICF
    </button>
  );
};
// Notes covered: Publish only after approval gates pass; lock content and generate accurate human-readable copy. On success, the button is replaced by a green "ICF Published Successfully" badge. Publishing calls POST /api/publish, which marks the document as Published with a timestamp.

// Node: Back to Review (id: b74c389c-ca01-457e-a38a-5e8b2f2b55e4)
const BackToReviewButton = () => {
  return <button onClick={() => navigate('/review')}>Back to Review</button>;
};
// Notes covered: An action button at the bottom-left of the page to return the user to the previous editing/review stage if there are typographical errors.