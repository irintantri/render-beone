/**
 * Handles the manual refinement and AI-assisted rewrite logic.
 */
export const AIAssistantModal = ({ section, onClose }) => {
  // State for the textarea input
  const [sectionContent, setSectionContent] = useState(section.content);
  
  // Validation: Ensure content is not empty before allowing AI trigger
  const isContentValid = sectionContent.trim().length > 0;

  const handleManualChange = (e) => {
    setSectionContent(e.target.value);
  };

  return (
    <div className="ai-assistant-modal">
      <h3>Section - {section.number}. {section.title}</h3>
      
      <textarea 
        value={sectionContent}
        onChange={handleManualChange}
        placeholder="Edit section content manually..."
      />
      
      {!isContentValid && (
        <span className="error-text">Content cannot be empty.</span>
      )}

      <div className="actions">
        <button onClick={onClose}>Cancel</button>
        <button 
          disabled={!isContentValid}
          onClick={() => triggerAIRewrite(sectionContent)}
        >
          Ask AI to Refine
        </button>
      </div>
    </div>
  );
};