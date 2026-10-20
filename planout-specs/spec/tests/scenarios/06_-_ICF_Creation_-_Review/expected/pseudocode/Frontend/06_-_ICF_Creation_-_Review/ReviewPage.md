import { useQuery } from 'react-query';

/**
 * Main Review Page Component
 * Orchestrates the layout for reviewing an ICF document.
 */
export const ReviewPage = ({ documentId }) => {
  // Fetch document data
  const { data: document, isLoading: isDocLoading } = useQuery(['document', documentId], () => 
    fetch(`/api/documents/${documentId}`).then(res => res.json())
  );

  // Fetch audit trail
  const { data: auditLogs, isLoading: isAuditLoading } = useQuery(['audit', documentId], () => 
    fetch(`/api/documents/${documentId}/audit`).then(res => res.json())
  );

  if (isDocLoading) return <LoadingSpinner />;

  return (
    <div className="review-page-layout">
      <GlobalNavigationHeader />
      <WrapperShell protocol_id={document.protocol_id} icf_name={document.icf_name} />
      <ProgressStepper />
      
      <main className="review-content-grid">
        <TableOfContents content={document.content} />
        
        <section className="document-viewer">
          {/* Render document sections as cards */}
          {parseSections(document.content).map((section) => (
            <DocumentSectionCard 
              key={section.id} 
              title={section.title} 
              content={section.body} 
              isAiGenerated={section.metadata?.is_ai_generated} 
            />
          ))}
        </section>

        <aside className="right-panel">
          <CommentActions />
          <AuditTrail logs={auditLogs} />
        </aside>
      </main>

      <BottomBarReview />
    </div>
  );
};