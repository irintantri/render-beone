// Node: Search (7393433d-01c1-443c-86e1-1f60a9339e6e)
// Description: Search box with icon and placeholder "Search protocols, ICF…".
// Logic: Instant search on character input.
// State: 
//   - `query`: string (bound to input)
//   - `isSearching`: boolean
//   - `results`: DashboardRow[]
// Validation: Triggered immediately on change.
// API Call: 
//   - If `query` is empty: Fetch default list via `GET /api/protocol`.
//   - If `query` has value: Call `GET /api/search` with `protocolName` and `ICFName` set to `query`.
// Cross-lane seam: Sends `protocolName` and `ICFName` to Logic lane via `GET /api/search`.
// Happy Path: User types, results update instantly, clearing input resets to default list.
// Empty State: Show "No results found" if API returns empty array.
// Notes covered: Search box; Text input with search icon; Placeholder "Search protocols, ICF…"; Search is instant as user types; Hook switches from sorted list to search endpoint; Matches against protocol name and ICF name; Clearing search reverts to sorted list.