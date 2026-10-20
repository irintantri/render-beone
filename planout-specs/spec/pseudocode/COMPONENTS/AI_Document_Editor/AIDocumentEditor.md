// Main container component for the AI editing panel
Component AIDocumentEditor(sectionData) {
    State instructionText = ""
    State currentContent = sectionData.content
    State isProcessing = false

    // Asset: assets/7c11f251-c8d8-47c5-8ea4-53cf3845db53.svg
    
    Function handleQuickPromptSelect(promptText) {
        instructionText = promptText
    }

    Function handleAskAI() {
        isProcessing = true
        
        // 1. Save manual changes first
        await saveSectionContent(sectionData.id, currentContent)
        
        // 2. Call AI Logic
        try {
            updatedContent = await AIService.rewriteSection(sectionData.id, currentContent, instructionText)
            
            // 3. Update local state for instant UI feedback
            currentContent = updatedContent
            updateGlobalSectionState(sectionData.id, updatedContent)
        } finally {
            isProcessing = false
        }
    }

    Render {
        SectionHeader(sectionData.title)
        
        // Editable content area
        TextArea(value=currentContent, onChange=(val) => currentContent = val)
        
        // Quick Prompts
        QuickPrompts(onSelect=handleQuickPromptSelect)
        
        // Instruction Input
        TextArea(
            placeholder="Ask AI to refine content, simplify language, check compliance…",
            value=instructionText,
            onChange=(val) => instructionText = val
        )
        
        // Action Button
        Button(
            label=isProcessing ? "Asking…" : "Ask AI",
            disabled=isProcessing || instructionText.isEmpty(),
            onClick=handleAskAI
        )
    }
}