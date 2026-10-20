COMPONENT EditActionBar(documentId, sectionId, sectionContent, onUpdateSuccess)
  STATE isEditing = false
  STATE isDeleteModalOpen = false
  STATE isPreviewModalOpen = false

  // Handlers
  FUNCTION handleEditClick() -> SET isEditing = true
  FUNCTION handleCancelEdit() -> SET isEditing = false
  
  FUNCTION handleSave()
    CALL API.updateSection(sectionId, { content: localContent })
    SET isEditing = false
    TRIGGER onUpdateSuccess()

  FUNCTION handleDeleteRequest() -> SET isDeleteModalOpen = true
  
  FUNCTION handlePreview() -> SET isPreviewModalOpen = true

  // Render
  RENDER
    Container(Asset: assets/116d52e2-ece5-423b-9cc7-f887580bde74.svg)
      Display DocumentName(documentId)
      Display ICFVersion(version)
      Display SelectedSectionTitle(sectionId)
      
      IF NOT isEditing
        Button("Preview Draft", onClick: handlePreview)
        Button("Edit", onClick: handleEditClick)
        Button("Delete", onClick: handleDeleteRequest)
      ELSE
        Button("Save", onClick: handleSave)
        Button("Cancel", onClick: handleCancelEdit)

    IF isDeleteModalOpen
      DeleteConfirmationModal(
        onConfirm: () => { 
          CALL API.deleteSection(sectionId)
          SET isDeleteModalOpen = false
          TRIGGER onUpdateSuccess() 
        },
        onCancel: () => SET isDeleteModalOpen = false
      )

    IF isPreviewModalOpen
      PreviewModal(
        documentId: documentId,
        onClose: () => SET isPreviewModalOpen = false
      )