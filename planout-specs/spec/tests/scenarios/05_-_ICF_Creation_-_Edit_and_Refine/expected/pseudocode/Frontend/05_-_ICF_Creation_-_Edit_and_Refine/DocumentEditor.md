import { useDocument } from './hooks/useDocument';

/**
 * Main container for the ICF Edit and Refine feature.
 * Asset: assets/ecabe235-1192-4f14-bb90-3389f1275208.svg
 */
export const DocumentEditor = ({ documentId }) => {
  const { document, isLoading, error } = useDocument(documentId);

  if (isLoading) return <Spinner />;
  if (error) return <ErrorMessage message="Failed to load document" />;

  return (
    <div className="editor-shell">
      <GlobalNavigationHeader />
      <ProgressStepper />
      <div className="editor-layout">
        <TableOfContents content={document.content} />
        <main className="document-sections">
          {document.content.sections.map((section) => (
            <SectionCard 
              key={section.id} 
              section={section} 
              onEditWithAI={() => openAIAssistant(section)} 
            />
          ))}
        </main>
        <EditActions />
      </div>
      <BottomBarEdit />
    </div>
  );
};