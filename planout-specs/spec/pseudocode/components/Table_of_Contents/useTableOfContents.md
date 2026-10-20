// Logic hook to manage TOC state and interactions
hook useTableOfContents(documentSections) {
    // State to track which section is currently in view
    state activeSectionId = null;

    // Helper to determine if a title is a sub-section (e.g., "3.1")
    function isSubSection(title) {
        return title matches regex /\d+\.\d+/;
    }

    // Process sections into a hierarchical structure for the UI
    computed tocItems = documentSections.map((section, index) => {
        return {
            id: section.id,
            label: section.title,
            isSubItem: isSubSection(section.title),
            displayNumber: isSubSection(section.title) ? section.title : (index + 1)
        };
    });

    // Interaction: Scroll to section and update active state
    function handleSectionClick(sectionId) {
        activeSectionId = sectionId;
        
        // Trigger browser scroll to the specific DOM element
        element = document.getElementById(`section-${sectionId}`);
        element.scrollIntoView({ behavior: 'smooth', block: 'start' });
        
        // Notify parent/right panel to load section details
        emit('loadSectionIntoRightPanel', sectionId);
    }

    return { tocItems, activeSectionId, handleSectionClick };
}