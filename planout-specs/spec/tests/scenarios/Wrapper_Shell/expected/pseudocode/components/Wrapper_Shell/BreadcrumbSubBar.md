// Sub-component for the breadcrumb logic
// Handles conditional rendering based on the presence of protocol data

COMPONENT BreadcrumbSubBar(props):
    // Props: protocolId, icfName, icfVersion
    
    DIV class="breadcrumb-container":
        // Dashboard link is always present
        RENDER Link("Dashboard")
        
        // Separator
        RENDER Icon("chevron-right")
        
        // Static label for the flow
        RENDER Label("Consent Creation")
        
        // Conditional rendering for dynamic protocol data
        IF props.protocolId:
            RENDER Pill(props.protocolId)
            
        IF props.icfName:
            RENDER Text(props.icfName)
            
        IF props.icfVersion:
            RENDER Pill(props.icfVersion)