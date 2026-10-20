export const SectionCard = ({ section, onEditWithAI }) => {
  const [isGenerating, setIsGenerating] = useState(false);

  return (
    <div className="section-card">
      <div className="header">
        <span className="title">
          {section.number}. {section.title}
        </span>
        {section.isAiGenerated && <Badge icon="sparkles">AI Generated</Badge>}
        <button onClick={onEditWithAI}>
          <Icon name="sparkles" /> Edit with AI
        </button>
      </div>
      
      <div className="body">
        {isGenerating && (
          <div className="ai-overlay">
            <Spinner />
            <p>AI is updating this section…</p>
          </div>
        )}
        <IcfMarkdown content={section.content} />
      </div>
    </div>
  );
};