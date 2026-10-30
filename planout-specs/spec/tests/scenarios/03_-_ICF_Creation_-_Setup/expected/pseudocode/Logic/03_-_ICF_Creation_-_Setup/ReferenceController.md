// Node: Fetch DMS (e.b7035f90-9384-4067-8189-cff37de1655a) / GET /api/reference?protocolId= (e.0c7f6808-4ec3-4ae9-9ee3-268172bd45b2)
// Receives: 'protocolId' from Frontend (Reference Documents).
// Logic: Check if 'protocolId' is present; if null, return 400 error "Select a protocol first". Query ReferenceDocument where protocol_id matches.
// Returns: Document Upload Schema (filtered list) to Data.
// Notes covered: Calls GET /api/reference?protocolId={selectedProtocol.protocol_id}, Finds a matching document by doc_kind or falls back to the first available, On success records the file name as attached, Requires a protocol to be selected first (shows error if not), The API returns a data reference payload filtered by the selected protocol ID.

// Node: Upload Reference (e.fa8d73e9-775a-4896-a7aa-b16b3f92e9a1) / POST /api/reference/{protocolId}/upload (e.f0ba8207-642b-404e-8a09-1903a9269049)
// Receives: File blob and 'doc_kind' from Frontend (Reference Documents).
// Logic: Validate file type (pdf, doc, docx, txt, md). Store file in bucket, create ReferenceDocument record with protocol_id, doc_kind, file_name, bucket_name, and current timestamp.
// Returns: Document Upload Schema (metadata) to Data.
// Notes covered: Opens a hidden file input (accept=".pdf,.doc,.docx,.txt,.md"), On file selection calls POST /api/reference/{protocolId}/upload with the file blob and doc_kind form field, The server responds with the uploaded document metadata.