// UI Component for the left panel
Asset: assets/cda38507-0965-4a06-a64e-588f5c095287.svg

component TableOfContents(props) {
    const { tocItems, activeSectionId, handleSectionClick } = useTableOfContents(props.sections);

    return (
        <nav class="toc-container">
            <h3>Table of Contents</h3>
            <ul>
                {tocItems.map(item => (
                    <li 
                        key={item.id}
                        class={item.isSubItem ? 'toc-sub-item' : 'toc-main-item'}
                        data-active={activeSectionId === item.id}
                        onClick={() => handleSectionClick(item.id)}
                    >
                        <span class="toc-number">{item.displayNumber}</span>
                        <span class="toc-label">{item.label}</span>
                    </li>
                ))}
            </ul>
        </nav>
    );
}