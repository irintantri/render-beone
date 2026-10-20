/**
 * Handles retrieval and searching of protocols for the selection wizard.
 */
async function fetchAllProtocols() {
  // GET /api/catalog/protocols
  return await api.get('/api/catalog/protocols');
}

async function searchProtocols(query) {
  if (query.length < 3) return [];
  // GET /protocol/search?q={query}
  return await api.get(`/protocol/search?q=${encodeURIComponent(query)}`);
}