/**
 * Component: TableOfContents
 * Asset: assets/cda38507-0965-4a06-a64e-588f5c095287.svg
 */
Component TableOfContents(props: { sections: Section[], activeSectionId: string }) {
    // Node: Protocol ID (7252f0b8-13a9-45c3-8063-27afbbc3d7e1)
    // Requirement: Render doc.protocol_id as a monospaced pill badge.
    Render PillBadge(text: doc.protocol_id, style: "monospaced")

    // Node: Table of Contents (5da9bb83-d80f-41a8-a07e-8914c66cb8e1)
    // Requirement: Render sections as clickable items.
    // Logic: 
    // 1. If title matches regex `\d+\.\d+`, render as sub-item (indented).
    // 2. Else, render as top-level item numbered by position.
    // 3. Active state: highlight if section.id === activeSectionId.
    ForEach section in props.sections {
        Render TOCItem(
            label: section.title,
            isIndented: section.title matches /\d+\.\d+/,
            isActive: section.id === props.activeSectionId,
            onClick: () => {
                // Cross-lane seam: Trigger scroll to Document Section Cards
                EmitEvent("SCROLL_TO_SECTION", { sectionId: section.id })
            }
        )
    }

    // Node: Footer (1aa0a071-872c-4845-89ef-8c3d9d79098d)
    // Requirement: Show ICF version and total section count.
    Render Footer(version: doc.icf_version, count: props.sections.length)
}
// Notes covered: Protocol ID (monospaced pill), Table of Contents (clickable, regex numbering, indentation, active state, scroll trigger), Footer (version, count).