// Component: AI-Assistant
// Asset: assets/7c11f251-c8d8-47c5-8ea4-53cf3845db53.svg

Component AIDocumentEditor {
  State: promptText = ""
  State: isProcessing = false
  State: sectionContent = { id, title, body }

  // Node: Select Section (id: ca6dea75-054d-45b6-8d45-96c437d88fe5)
  Render SectionDisplay {
    Label: "Section - {sectionContent.id}. {sectionContent.title}"
    Textarea: bind(sectionContent.body) // Editable by user
  }

  // Node: Quick Prompts (id: ea132e46-80c7-4c27-b791-b7e8b7006a08)
  Render QuickPrompts {
    Button("Simplify language for patient readability") -> onClick: setPromptText("Simplify language for patient readability")
    Button("Add plain-language summary.") -> onClick: setPromptText("Add plain-language summary.")
    // Note: Ambiguity - Only two prompts provided in description, but requirement says "three". 
    // Implementation: Defaulting to the two provided.
  }

  // Node: Add instruction (id: 019819c9-e8e6-475a-b310-98fbedc4c78f)
  Render InstructionTextarea {
    Textarea: bind(promptText)
    Placeholder: "Ask AI to refine content, simplify language, check compliance…"
  }

  // Node: Ask AI Button (id: 928ebd7b-a200-46f9-8bce-9c0781d09c3f)
  Render AskAIButton {
    Button: 
      Label: isProcessing ? "Asking…" : "Ask AI"
      Disabled: promptText.isEmpty() OR isProcessing
      OnClick: handleAskAI()
  }

  Function handleAskAI() {
    isProcessing = true
    // Trigger Logic Layer
    Response = Logic.requestAIRewrite(sectionContent, promptText)
    
    // Update UI
    sectionContent.body = Response.updatedText
    isProcessing = false
  }
}

// Notes covered: 
// Quick Prompts: Provide three quick-prompts, User can select one, fills Add Instruction textarea.
// Add instruction: Textarea with placeholder, natural-language prompt for AI.
// Ask AI Button: Display button, Primary/full-width, Disabled state, "Asking..." state, saves manual changes, calls rewrite endpoint, updates local state.
// Select Section: Label format, editable textarea.