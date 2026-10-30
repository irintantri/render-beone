/**
 * Component: DocumentSectionCards
 */
Component DocumentSectionCards(props: { sections: Section[] }) {
    // Node: Document Section Cards (2cbd4f4a-944c-4fa2-877c-426f8fa18611)
    // Requirement: Render each section as a card.
    ForEach section in props.sections {
        Card {
            Header {
                Text(section.number)
                Text(section.title.stripLeadingNumber(), style: "bold")
                If (section.isAiGenerated) {
                    Render Badge("AI Generated", icon: "sparkles")
                }
                Button("Edit with AI", icon: "sparkles", onClick: () => LoadIntoAiAssistant(section))
            }
            
            // Requirement: Body (read mode)
            If (section.isProcessing) {
                // Requirement: AI generating overlay
                Overlay {
                    Spinner()
                    Text("AI is updating this section…")
                }
            } Else {
                Render IcfMarkdown(content: section.content)
            }
        }
    }
}
// Notes covered: Header (number, title, AI badge, Edit button), Body (IcfMarkdown), AI generating overlay (spinner, message), Edit with AI action.