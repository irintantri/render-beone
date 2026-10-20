import { useEffect, useState } from 'react';

/**
 * Fetches document data using the authoritative API contract.
 */
export const useDocument = (id: string) => {
  const [document, setDocument] = useState(null);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchDocument = async () => {
      try {
        // GET /api/documents/:id
        const response = await fetch(`/api/documents/${id}`);
        if (!response.ok) throw new Error('Network response was not ok');
        const data = await response.json();
        setDocument(data);
      } catch (err) {
        setError(err);
      } finally {
        setIsLoading(false);
      }
    };

    fetchDocument();
  }, [id]);

  return { document, isLoading, error };
};

// ORPHAN_FIELD: sections (Nested within Document.content)
// ORPHAN_FIELD: isAiGenerated (Metadata flag for section cards)
// ORPHAN_FIELD: number (Section identifier)
// ORPHAN_FIELD: title (Section identifier)