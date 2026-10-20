// Custom hook to manage the real-time polling of the generation job
import { useState, useEffect } from 'react';

export const useGenerationPolling = (jobId: string) => {
  const [data, setData] = useState({ status: '', progress: 0, step_label: '', document_id: null });
  const [isComplete, setIsComplete] = useState(false);

  useEffect(() => {
    if (!jobId) return;

    const interval = setInterval(async () => {
      const response = await fetch(`/api/icf/generation/${jobId}`);
      const result = await response.json();
      
      setData(result);

      if (result.status === 'completed' || result.progress === 100) {
        setIsComplete(true);
        clearInterval(interval);
        // Auto-navigate to editor using document_id
        window.location.href = `/editor/${result.document_id}`;
      }
    }, 1000);

    return () => clearInterval(interval);
  }, [jobId]);

  return { ...data, isComplete };
};