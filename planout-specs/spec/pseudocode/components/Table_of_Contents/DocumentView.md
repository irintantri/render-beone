// Orchestrator component connecting TOC to the Document Section Cards
component DocumentView(documentData) {
    return (
        <div class="layout-wrapper">
            <aside class="left-panel">
                <TableOfContents sections={documentData.sections} />
            </aside>
            
            <main class="center-panel">
                {documentData.sections.map(section => (
                    <div id={`section-${section.id}`} class="section-card">
                        <DocumentSectionCard data={section} />
                    </div>
                ))}
            </main>

            <aside class="right-panel">
                <AISectionAssistant />
            </aside>
        </div>
    );
}