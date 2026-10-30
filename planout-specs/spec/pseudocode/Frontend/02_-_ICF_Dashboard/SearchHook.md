import { useState, useEffect } from 'react';

export const useSearch = () => {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);

  useEffect(() => {
    if (query.length > 0) {
      // Trigger: GET /api/search?protocolName={query}&ICFName={query}
      // Logic lane handles the filtering logic
    } else {
      // Revert to default list
    }
  }, [query]);

  return { query, setQuery, results };
};