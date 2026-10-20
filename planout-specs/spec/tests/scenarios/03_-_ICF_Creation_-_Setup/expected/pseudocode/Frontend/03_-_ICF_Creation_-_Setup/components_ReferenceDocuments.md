export const ReferenceDocuments = ({ protocolId, onAttach, onError }) => {
  const handleUpload = async (file, doc_kind) => {
    if (!protocolId) {
      onError("Select a protocol first");
      return;
    }
    
    const formData = new FormData();
    formData.append('file', file);
    formData.append('doc_kind', doc_kind);

    // POST /api/reference/{protocolId}/upload
    const response = await fetch(`/api/reference/${protocolId}/upload`, {
      method: 'POST',
      body: formData
    });

    if (response.ok) {
      const data = await response.json();
      onAttach(doc_kind, data);
    } else {
      onError("Upload failed");
    }
  };

  return (
    <div>
      {['Investigation Brochure', 'Lab Manual'].map(kind => (
        <div key={kind} className="upload-block">
          <h3>{kind}</h3>
          <button onClick={() => /* Open File Picker */}>Upload</button>
          <button onClick={() => /* Fetch from DMS */}>Fetch DMS</button>
          {/* Attached file tag logic here */}
        </div>
      ))}
      <p>Documents provide reference context for AI generation.</p>
    </div>
  );
};

// ORPHAN_FIELD: drug_code (referenced in Select Protocol description, not in schema)