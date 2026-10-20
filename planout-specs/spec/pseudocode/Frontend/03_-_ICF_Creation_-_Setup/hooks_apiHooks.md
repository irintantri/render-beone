import { useState, useEffect } from 'react';

export const useProtocolSearch = () => {
  const [protocols, setProtocols] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/catalog/protocols')
      .then(res => res.json())
      .then(data => { setProtocols(data); setLoading(false); });
  }, []);

  return { protocols, loading };
};

export const useTemplates = () => {
  const [templates, setTemplates] = useState([]);
  
  useEffect(() => {
    fetch('/api/catalog/templates')
      .then(res => res.json())
      .then(setTemplates);
  }, []);

  return { templates };
};