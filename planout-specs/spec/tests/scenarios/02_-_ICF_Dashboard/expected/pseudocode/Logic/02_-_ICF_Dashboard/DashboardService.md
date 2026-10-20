/**
 * API Route Handlers
 */

// GET /api/stats
// Returns dashboard metrics
handleGetStats = () => {
    return getDashboardStats();
};

// GET /api/protocol?sort_by=&sort_order=
// Returns sorted list of protocols
handleGetProtocols = (req) => {
    const { sort_by, sort_order } = req.query;
    return getProtocols(sort_by, sort_order);
};

// GET /api/search?protocolName=&ICFName=
// Returns filtered list based on search input
handleSearch = (req) => {
    const { protocolName, ICFName } = req.query;
    return searchProtocols(protocolName, ICFName);
};