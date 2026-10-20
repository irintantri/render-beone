/**
 * Orchestrates state transitions for the ICF Setup Wizard.
 */
class ICFSetupController {
  state = {
    selectedProtocol: null,
    selectedTemplate: null,
    attachedDocuments: {
      "Investigation Brochure": null,
      "Lab Manual": null
    }
  };

  async handleProtocolSelection(protocol) {
    this.state.selectedProtocol = protocol;
    // Trigger fetch of reference docs for the new protocol
    this.state.attachedDocuments = await fetchReferenceDocuments(protocol.protocol_id);
  }

  async handleFileUpload(docKind, file) {
    if (!this.state.selectedProtocol) {
      throw new Error("Select a protocol first");
    }
    const uploadedDoc = await uploadReferenceDocument(
      this.state.selectedProtocol.protocol_id, 
      file, 
      docKind
    );
    this.state.attachedDocuments[docKind] = uploadedDoc;
  }
}