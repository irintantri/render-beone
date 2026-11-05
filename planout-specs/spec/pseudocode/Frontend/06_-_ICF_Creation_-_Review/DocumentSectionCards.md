/**
 * Node: Document Section Cards (52049b0f-baf8-46c4-846e-c9c20e875297)
 * Description: Renders document sections as individual cards.
 * Inputs: Receives 'content' (JSON/Markdown string) from GET /api/documents/:id (Logic lane).
 */

Component DocumentSectionCards(props: { documentId: string }) {
  // State: Fetch document data from Logic lane
  const { data, isLoading, error } = useQuery({
    queryKey: ['document', props.documentId],
    queryFn: () => fetch('GET /api/documents/:id', { params: { id: props.documentId } })
  });

  // Logic: Parse 'content' field from Document entity
  // Assuming 'content' is a structured JSON string containing sections
  const sections = JSON.parse(data.content || '[]');

  if (isLoading) return <Spinner />;
  if (error) return <ErrorMessage message="Failed to load document sections" />;

  return (
    <div className="section-container">
      {sections.map((section) => (
        <Card key={section.id}>
          <CardHeader>
            <span className="section-number">{section.number}</span>
            <span className="section-title"><strong>{stripLeadingNumber(section.title)}</strong></span>
            {section.isAiGenerated && (
              <Badge className="ai-label">
                <SparklesIcon /> AI Generated <!-- ORPHAN_FIELD: isAiGenerated -->
              </Badge>
            )}
          </CardHeader>
          <CardBody>
            <IcfMarkdown content={section.body} />
          </CardBody>
        </Card>
      ))}
    </div>
  );
}

/**
 * Helper: Strips leading numbers (e.g., "1. Introduction" -> "Introduction")
 */
function stripLeadingNumber(title: string): string {
  return title.replace(/^\d+\.\s*/, '');
}

// Notes covered:
// - Render document per section as a card.
// - Header: Section number, bold section title (leading number stripped).
// - AI label badge with sparkles icon if present.
// - Body: Read mode using IcfMarkdown component.