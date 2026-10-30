// Node: Select Template (e.fd9f98b3-1067-45a8-b088-b8a70626838f) / GET /api/catalog/templates (e.3e8a0bbc-5bbd-4df5-a592-28c1978b7a87)
// Receives: Trigger on page load from Frontend (Select Template).
// Logic: Fetch all records from Template entity.
// Returns: TemplateDTO to Data.
// Notes covered: Calls 'GET /api/catalog/templates' on load of the page to see ICF template pick-list, The API returns template data from the database, providing the frontend with a set of available sample document templates.

<!-- API_PAYLOAD
{
  "GET /protocol/search": {
    "request": {
      "body": [
        { "name": "q", "type": "string", "source": "Protocol.protocolName" }
      ]
    },
    "responses": {
      "200": { "body": ["data", "meta"], "from": "Protocol" }
    }
  },
  "GET /api/catalog/protocols": {
    "request": {
      "body": []
    },
    "responses": {
      "200": { "body": ["data"], "from": "Protocol" }
    }
  }
}
-->