/**
 * Node: GET /protocol/search?q= (e56db925-48a0-4e01-a357-bae8014e7ce5)
 * Triggered by: Search Protocol (Frontend)
 * Consumed by: Protocol Search Schema (Data)
 */
async function searchProtocols(query: string) {
  // Validation: Ensure query length >= 3 characters
  if (!query || query.length < 3) {
    return { data: [], meta: { query, totalResults: 0 } };
  }

  // Happy Path: Query Protocol entity for matches on protocolName or protocolId
  const results = await db.Protocol.findMany({
    where: {
      OR: [
        { protocolName: { contains: query, mode: 'insensitive' } },
        { protocolId: { contains: query, mode: 'insensitive' } }
      ]
    }
  });

  return {
    data: results,
    meta: { query, totalResults: results.length }
  };
}

// Notes covered:
// - Calls GET /protocol/search?q= when user enters at least 3 characters.
// - Endpoint is for search protocol by name or protocol ID.
// - Returns the protocol search JSON schema.

/**
 * Node: GET /api/catalog/protocols (3ece0980-910d-42a3-ab1a-c5962426d73d)
 * Triggered by: Select Protocol (Frontend)
 * Consumed by: ProtocolOption Schema (Data)
 */
async function getProtocolCatalog() {
  // Happy Path: Fetch all protocols from the catalog
  const protocols = await db.Protocol.findMany({
    select: {
      protocolId: true,
      protocolName: true,
      phase: true,
      category: true,
      description: true,
      status: true,
      lastModified: true
    }
  });

  // Return formatted ProtocolOption schema
  return { data: protocols };
}

// Notes covered:
// - Load full protocol list from the file-backed catalog API.
// - Used for the selection panel on page load.
// - Returns ProtocolOption schema.