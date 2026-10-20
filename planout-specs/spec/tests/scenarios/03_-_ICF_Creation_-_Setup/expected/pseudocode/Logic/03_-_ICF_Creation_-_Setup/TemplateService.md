/**
 * Manages ICF template retrieval.
 */
async function getAvailableTemplates() {
  // GET /api/catalog/templates
  return await api.get('/api/catalog/templates');
}