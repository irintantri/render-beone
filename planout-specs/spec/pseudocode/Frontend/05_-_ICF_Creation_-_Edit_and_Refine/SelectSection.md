// Node: Select Section (25057fce-bbf2-4a3f-860d-c9efb61bcf0e)

Component SelectSection:
  Props: sectionData (Object)
  State: editableContent (string)

  Effect: Initialize editableContent with sectionData.content

  Render:
    - Label: "Section - {sectionData.number}. {sectionData.title}"
    - Textarea: 
        Value: editableContent
        OnChange: Update editableContent
        Validation: Immediate check for empty state (disable AI trigger if empty)

  Notes covered: Display Section label, textarea with current content, manual adjustment capability.