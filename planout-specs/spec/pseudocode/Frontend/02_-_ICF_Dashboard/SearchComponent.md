// Node: Search (7393433d-01c1-443c-86e1-1f60a9339e6e)
// Description: Search box with icon and placeholder "Search protocols, ICF…".
// Validation: Instant search as user types.
// Logic: 
//   - On input change: update local state `query`.
//   - If `query` is not empty: call GET /api/search with `protocolName` and `ICFName` set to `query`.
//   - If `query` is empty: revert to default sorted list endpoint.
// Cross-lane: Calls "on search" (d4fe475f-afe4-4601-bef2-f3305e96c104) in Logic lane.
// Happy Path: User types -> API returns matching DashboardRow entities -> Table updates.
// Empty State: No results found -> Display "No protocols found" message.
// Notes covered: Search box; Text input with search icon; Placeholder "Search protocols, ICF…"; Search is instant as user types; Hook switches from sorted list to search endpoint; Matches against protocol name and ICF name; Clearing search reverts to sorted list.