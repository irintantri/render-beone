/**
 * API Endpoints for the ICF Dashboard
 */

// GET /api/stats
// Returns: DashboardStats DTO
controller.get('/api/stats', async (req, res) => {
  const stats = await getDashboardStats();
  res.json(stats);
});

// GET /api/protocol
// Query Params: sort_by, sort_order
// Returns: Array of DashboardRow DTOs
controller.get('/api/protocol', async (req, res) => {
  const { sort_by, sort_order } = req.query;
  const protocols = await getProtocolList(sort_by, sort_order);
  res.json({ data: protocols });
});

// GET /api/search
// Query Params: protocolName, ICFName
// Returns: Array of DashboardRow DTOs
controller.get('/api/search', async (req, res) => {
  const { protocolName, ICFName } = req.query;
  const results = await searchProtocols(protocolName, ICFName);
  res.json({ data: results });
});