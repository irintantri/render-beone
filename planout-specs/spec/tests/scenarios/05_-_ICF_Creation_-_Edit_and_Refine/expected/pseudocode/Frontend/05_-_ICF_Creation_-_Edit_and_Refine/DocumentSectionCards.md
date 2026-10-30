// Node: Document Section Cards (2f188edc-72f5-4eee-bf6a-b542a4f55df3)
// Asset: assets/ecabe235-1192-4f14-bb90-3389f1275208.svg

Component DocumentSectionCards:
  Props: documentId (uuid)
  State: sections (Array), loading (boolean), aiProcessing (boolean)

  Effect: On mount, call GET /api/documents/:id with {id: documentId}
    - Success: Set sections from response.content (parsed into sections)
    - Error: Display error toast

  Render:
    For each section in sections:
      Card:
        Header:
          - Text: "{section.number}. {section.title}" (Bold)
          - Badge: "AI Generated" (if section.is_ai_generated <!-- ORPHAN_FIELD: is_ai_generated -->)
          - Button: "Edit with AI" (onClick: trigger Select Section)
        Body:
          - If aiProcessing: Overlay with spinner + "AI is updating this section…"
          - Else: <IcfMarkdown content={section.content} />

  Notes covered: Render document per section, Header details (number, title, badge, button), Body (read mode), IcfMarkdown usage, AI generating overlay, Edit with AI button trigger.