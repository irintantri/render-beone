// Node: Document Section Cards (2f188edc-72f5-4eee-bf6a-b542a4f55df3)
// Asset: assets/ecabe235-1192-4f14-bb90-3389f1275208.svg

Component DocumentSectionCards:
  State: documentData (from GET /api/documents/:id)
  
  Render:
    For each section in documentData.content:
      Card:
        Header:
          - Text: Section number + Title (stripped of leading number, bold)
          - Badge: "AI Generated" + sparkles icon (conditional: if metadata.is_ai_generated <!-- ORPHAN_FIELD: is_ai_generated -->)
          - Button: "Edit with AI" (sparkles icon) -> onClick: trigger Select Section(section)
        Body:
          - If isProcessing: Overlay(spinner, "AI is updating this section…")
          - Else: IcfMarkdown(section.content)

  Notes covered: Render document per section, Header components (number, title, badge, button), Body (read mode, IcfMarkdown), AI generating overlay (spinner, message), Edit with AI button trigger.