/**
 * Component: DocumentGenerationForm
 * Purpose: Collects template and source data to trigger AI-powered document generation.
 */

import { useState } from 'react';
import { useDocumentGeneration } from './hooks/useDocumentGeneration';

export const DocumentGenerationForm = () => {
  // State management for API payload fields
  const [template_id, setTemplateId] = useState('');
  const [source_filename, setSourceFilename] = useState('');
  const [values, setValues] = useState({}); // JSON object for template variables

  const { generateDocument, loading, error } = useDocumentGeneration();

  const handleSubmit = async () => {
    // Validation: Ensure required fields are present before submission
    if (!template_id || !source_filename) {
      console.error("Validation Error: template_id and source_filename are required.");
      return;
    }

    await generateDocument({
      template_id,
      source_filename,
      values
    });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        placeholder="Template ID" 
        value={template_id} 
        onChange={(e) => setTemplateId(e.target.value)} 
      />
      <input 
        placeholder="Source Filename" 
        value={source_filename} 
        onChange={(e) => setSourceFilename(e.target.value)} 
      />
      {/* JSON input for values */}
      <button disabled={loading}>Generate Document</button>
    </form>
  );
};