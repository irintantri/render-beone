/**
 * Logic for managing the ICF Dashboard data retrieval, 
 * sorting, and searching operations.
 */

// Fetch dashboard summary statistics
function getDashboardStats() {
    // Query Protocol table for counts based on status
    // Returns: { total: count, inReview: count, approved: count }
    // <!-- MISSING_FIELD: Protocol.status_category -->
    return database.Protocol.aggregate({
        total: count(),
        inReview: count(status == 'In Review'),
        approved: count(status == 'Approved')
    });
}

// Fetch and sort protocol list
function getProtocols(sortBy, sortOrder) {
    // Fetch Protocol joined with ICF and ICFFile
    // Sort by provided field and order
    return database.Protocol.findMany({
        include: { ICF: { include: { ICFFile: true } } },
        orderBy: { [sortBy]: sortOrder }
    });
}

// Search across protocols and ICFs
function searchProtocols(protocolName, icfName) {
    // Perform case-insensitive search across joined entities
    return database.Protocol.findMany({
        where: {
            OR: [
                { name: { contains: protocolName } },
                { ICF: { name: { contains: icfName } } }
            ]
        },
        include: { ICF: { include: { ICFFile: true } } }
    });
}