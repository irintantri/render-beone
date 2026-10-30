/**
 * Node: Protocol Search Schema (5c296867-a41c-4c4a-910a-39beaf439c61)
 * Interface for GET /protocol/search?q=
 */
interface ProtocolSearchResponse {
  data: Array<{
    protocolId: string;
    protocolName: string;
    phase: string;
    category: string;
    description: string;
    lastModified: string; // ISO 8601
  }>;
  meta: {
    query: string;
    totalResults: number;
  };
}

// Notes covered: Protocol search JSON schema structure, protocolId, protocolName, phase, category, description, lastModified, meta query, totalResults.

/**
 * Node: Document Upload Schema (d701f07c-1733-471d-8ba7-133a3c27c4a5)
 * Interface for GET /api/reference?protocolId= and POST /api/reference/{protocolId}/upload
 */
interface ReferenceUploadResponse {
  status: "success";
  message: "Document uploaded successfully";
  reference: {
    id: string;
    protocol_id: string;
    doc_kind: string;
    file_name: string;
    bucket_name: string;
    uploaded_at: string; // ISO 8601 date-time
  };
}

// Notes covered: status must be "success", message must be "Document uploaded successfully", reference object fields (id, protocol_id, doc_kind, file_name, bucket_name, uploaded_at), additionalProperties false, schema draft 2020-12.

/**
 * Node: TemplateDTO (6a575d4a-681e-438a-b864-89890201491b)
 * Interface for GET /api/catalog/templates
 */
interface TemplateDTO {
  id: string;
  name: string;
  description: string;
  recommended: boolean;
}

// Notes covered: TemplateDTO fields (id, name, description, recommended).

/**
 * Node: ProtocolOption Schema (5dde8ffc-942a-4777-9f23-a78f8276acfd)
 * Interface for GET /api/catalog/protocols
 */
interface ProtocolOptionResponse {
  data: Array<{
    protocolId: string;
    protocolName: string;
    phase: string;
    category: string;
    description: string;
    status: string;
    lastModified: string; // ISO 8601
  }>;
}

// Notes covered: ProtocolOption schema structure, protocolId, protocolName, phase, category, description, status, lastModified.