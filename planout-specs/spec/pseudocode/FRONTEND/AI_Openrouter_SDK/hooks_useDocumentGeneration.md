/**
 * Hook: useDocumentGeneration
 * Purpose: Handles the API interaction for document generation via OpenRouter SDK.
 */

import { useState } from 'react';

export const useDocumentGeneration = () => {
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const generateDocument = async (payload) => {
    setLoading(true);
    setError(null);

    try {
      const response = await fetch('/generate-document', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          template_id: payload.template_id,
          source_filename: payload.source_filename,
          values: payload.values
        })
      });

      if (!response.ok) throw new Error('Failed to generate document');

      const data = await response.json();
      
      // Data returned: id, filled_markdown, pages
      return data;
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  return { generateDocument, loading, error };
};