/**
 * Handles retrieval of catalog data for the ICF Setup wizard.
 */
class CatalogController {
  
  // GET /api/catalog/protocols
  // Returns list of all available protocols for initial selection
  async getProtocols(req, res) {
    const protocols = await db.Protocol.findAll();
    res.json({ data: protocols });
  }

  // GET /protocol/search?q={query}
  // Returns filtered protocols based on search string
  async searchProtocols(req, res) {
    const { q } = req.query;
    const results = await db.Protocol.findByNameOrId(q);
    res.json({ 
      data: results,
      meta: { query: q, totalResults: results.length }
    });
  }

  // GET /api/catalog/templates
  // Returns available ICF templates
  async getTemplates(req, res) {
    const templates = await db.Template.findAll();
    res.json({ data: templates });
  }
}