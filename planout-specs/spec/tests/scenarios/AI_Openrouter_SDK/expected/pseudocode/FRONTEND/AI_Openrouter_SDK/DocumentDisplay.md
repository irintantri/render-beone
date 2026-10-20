/**
 * Component: DocumentDisplay
 * Purpose: Renders the result of the DocumentGeneration process.
 */

export const DocumentDisplay = ({ documentData }) => {
  // Expects object containing: id, filled_markdown, pages
  return (
    <div>
      <h1>Document ID: {documentData.id}</h1>
      <p>Total Pages: {documentData.pages}</p>
      <div className="markdown-content">
        {documentData.filled_markdown}
      </div>
    </div>
  );
};