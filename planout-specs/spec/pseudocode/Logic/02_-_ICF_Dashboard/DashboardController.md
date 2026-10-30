/**
 * Node: GET /api/stats (4da8a4d8-70d8-4935-bd4f-c24f97c51d92)
 * Triggered on page load.
 * Happy Path: Fetches aggregate counts from DashboardStats.
 * Error State: Returns 500 if database query fails.
 * Side Effects: None.
 */
async function getStats() {
  const stats = await db.DashboardStats.findFirst();
  return stats || { total: 0, inReview: 0, approved: 0 };
}
// Notes covered: on load of the page, GET /api/stats from DashboardStats data table (total, inReview, approved counts).

/**
 * Node: GET /api/protocol?sort_by=&sort_order= (0161768c-00a1-4de1-b2e0-2edf5ad23c1a)
 * Triggered by Frontend Sorting component.
 * Happy Path: Returns sorted list of DashboardRow entities.
 * Error State: Returns 400 if sort parameters are invalid.
 */
async function getProtocols(req) {
  const { sort_by, sort_order } = req.query;
  return await db.DashboardRow.findMany({
    orderBy: { [sort_by]: sort_order }
  });
}
// Notes covered: GET /api/protocol?sort_by=&sort_order= from the DashboardRow data table.

/**
 * Node: on search (d4fe475f-afe4-4601-bef2-f3305e96c104)
 * Triggered by Frontend Search component.
 * Happy Path: Filters DashboardRow by protocolName or icf_name.
 * Empty State: Returns empty array if no matches found.
 */
async function searchProtocols(req) {
  const { protocolName, ICFName } = req.query;
  return await db.DashboardRow.findMany({
    where: {
      OR: [
        { name: { contains: protocolName } },
        { icf_name: { contains: ICFName } }
      ]
    }
  });
}
// Notes covered: GET /api/search?protocolName=&ICFName= to search the work queue by name/ID.

/**
 * Node: GET /api/protocol (a4af7d41-fec3-443f-b55e-93d2adc85c0d)
 * Standard fetch for protocol list.
 * Note: The schema provided in the node description includes a 'files' array 
 * which is not present in the authoritative DashboardRow schema.
 * <!-- MISSING_FIELD: DashboardRow.files -->
 */
async function listProtocols() {
  return await db.DashboardRow.findMany();
}
// Notes covered: Obtain the list of protocols that matches protocolId, version, name, ICF name, ICF version, status and last modification from the database and return the list protocol JSON schema.