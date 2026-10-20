COMPONENT PreviewModal(documentId, onClose)
  // Full-screen overlay for PDF review
  RENDER
    Overlay
      Header
        Icon("Document")
        Text("{protocol_id} ICF — {icf_version}.pdf · Draft")
        Button("Close", onClick: onClose)
      Body
        ScrollableContainer
          // Renders the full document including AI overrides
          IcfPdfDocument(documentId: documentId)
      // Dismissal logic
      Backdrop(onClick: onClose)