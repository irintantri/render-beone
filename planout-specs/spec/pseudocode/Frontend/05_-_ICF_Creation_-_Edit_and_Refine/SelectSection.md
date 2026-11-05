// Node: Select Section (25057fce-bbf2-4a3f-860d-c9efb61bcf0e)

Component SelectSection:
  Props: selectedSection (from Document Section Cards)
  State: editableContent (initialized to selectedSection.content)

  Render:
    - Label: "Section - {number}. {title}"
    - Textarea: value={editableContent}, onChange={setEditableContent}
    - Helper: "Manually adjust content before AI processing"

  Notes covered: Display Section label, textarea with current content, manual adjustment capability.