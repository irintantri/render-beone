// Custom hook to manage protocol state and API interactions.
// Logic:
// 1. On mount, fetch all protocols via GET /api/catalog/protocols.
// 2. On search input change (>= 3 chars), call GET /protocol/search?q={q}.
// 3. Handle `selectedProtocol` state and CSS class toggling.
// 4. Handle `selectedTemplate` state.
// 5. Handle `ReferenceDocument` upload/fetch states.
// Notes covered: All API integration logic and state management.