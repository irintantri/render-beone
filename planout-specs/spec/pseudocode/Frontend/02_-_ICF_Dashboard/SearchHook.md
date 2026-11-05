import { useState, useEffect } from 'react';

export const useSearch = () => {
  const [query, setQuery] = useState('');
  const [data, setData] = useState([]);

  useEffect(() => {
    if (!query) {
      // Fetch default sorted list
      fetch('/api/protocol'); 
    } else {
      // Triggered by "on search" (d4fe475f-afe4-4601-bef2-f3305e96c104)
      fetch(`/api/search?protocolName=${query}&ICFName=${query}`);
    }
  }, [query]);

  return { query, setQuery, data };
};