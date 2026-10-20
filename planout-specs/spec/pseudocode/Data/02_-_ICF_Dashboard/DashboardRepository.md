/**
 * Data access layer for the ICF Dashboard.
 * Handles aggregation for stats and retrieval for the protocol work queue.
 */

function getDashboardStats() {
  // Query Protocol table to aggregate counts
  const total = db.Protocol.count();
  const inReview = db.Protocol.count({ where: { status: 'IN_REVIEW' } });
  const approved = db.Protocol.count({ where: { status: 'APPROVED' } });

  return { total, inReview, approved };
}

function getProtocolList(sortBy, sortOrder) {
  // Fetch protocols joined with ICF and File data
  // Apply sorting based on parameters
  return db.Protocol.findMany({
    orderBy: { [sortBy]: sortOrder },
    include: { icfs: { include: { files: true } } }
  });
}

function searchProtocols(protocolName, icfName) {
  // Filter protocols by name or associated ICF name
  return db.Protocol.findMany({
    where: {
      OR: [
        { name: { contains: protocolName } },
        { icfs: { some: { name: { contains: icfName } } } }
      ]
    },
    include: { icfs: { include: { files: true } } }
  });
}