/**
 * Renders individual document sections.
 * Asset: assets/a1745dc6-62ab-4081-95eb-18ec7b877997.svg
 */
export const DocumentSectionCard = ({ title, content, isAiGenerated }) => {
  return (
    <div className="section-card">
      <div className="section-header">
        <h3>{title}</h3>
        {isAiGenerated && <span className="badge-ai">AI Generated ✨</span>}
      </div>
      <div className="section-body">
        <IcfMarkdown content={content} />
      </div>
    </div>
  );
};