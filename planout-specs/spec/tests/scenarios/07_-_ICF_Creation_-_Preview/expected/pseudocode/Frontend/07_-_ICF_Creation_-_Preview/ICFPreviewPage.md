import React, { useState, useEffect } from 'react';
import { fetchDocument, fetchDocumentSections, publishDocument } from './api';

/**
 * ICF Preview Page
 * Asset: assets/296abc29-be91-4796-bd36-496013ee60e5.svg
 */
export const ICFPreviewPage = ({ documentId }) => {
  const [document, setDocument] = useState(null);
  const [sections, setSections] = useState([]);
  const [isPublished, setIsPublished] = useState(false);
  const [isLoading, setIsLoading] = useState(true);
  
  // ORPHAN_FIELD: zoomLevel
  // ORPHAN_FIELD: pageCount

  useEffect(() => {
    const loadData = async () => {
      const doc = await fetchDocument(documentId);
      const sec = await fetchDocumentSections(documentId);
      setDocument(doc);
      setSections(sec.sort((a, b) => a.order - b.order));
      setIsLoading(false);
    };
    loadData();
  }, [documentId]);

  const handlePublish = async () => {
    const payload = {
      documentId: document.id,
      publishDate: new Date().toISOString()
    };
    
    const response = await publishDocument(payload);
    if (response.status === 'published') {
      setIsPublished(true);
    }
  };

  if (isLoading) return <div>Loading Preview...</div>;

  return (
    <div className="wrapper-shell">
      <GlobalNavigationHeader />
      <ProgressStepper />
      
      <div className="document-toolbar">
        <span>{document.title}</span> <!-- ORPHAN_FIELD: document filename -->
        <span>Pages: {pageCount}</span> <!-- ORPHAN_FIELD: pageCount -->
        <button>Zoom In</button> <!-- ORPHAN_FIELD: Zoom button -->
        <button>Zoom Out</button> <!-- ORPHAN_FIELD: Zoom button -->
      </div>

      <div className="icf-document-container" style={{ background: 'grey' }}>
        <div className="pdf-page" style={{ background: 'white' }}>
          <h1>INFORMED CONSENT FORM</h1>
          {sections.map(section => (
            <div key={section.id}>
              <h3>{section.order}. {section.title}</h3> <!-- ORPHAN_FIELD: section title -->
              <p>{section.content}</p>
            </div>
          ))}
        </div>
      </div>

      <div className="action-footer">
        <button onClick={() => window.history.back()}>Back to Review</button>
        
        {isPublished ? (
          <div className="badge-success">ICF Published Successfully</div>
        ) : (
          <button onClick={handlePublish}>Publish</button>
        )}
      </div>
    </div>
  );
};