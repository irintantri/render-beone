// Main layout component that wraps page content
// Asset: assets/e368bbe4-c879-4b9e-8c43-c542dee64bfc.svg

COMPONENT WrapperShell(children, protocolInfo, currentStep):
    
    // TopBar: Global navigation and user identity
    RENDER TopBar()

    // Breadcrumb sub-bar: Contextual navigation
    // Asset: assets/e368bbe4-c879-4b9e-8c43-c542dee64bfc.svg
    CONTAINER BreadcrumbSubBar:
        IF showDashboardLink:
            RENDER Link("Dashboard", to="/dashboard")
        
        RENDER Text("Consent Creation")
        
        IF protocolInfo.id:
            RENDER Pill(text=protocolInfo.id, type="protocol")
            
        IF protocolInfo.icfName:
            RENDER Text(protocolInfo.icfName)
            
        IF protocolInfo.icfVersion:
            RENDER Pill(text=protocolInfo.icfVersion, type="version")

    // Step Indicator: Visual progress for the 5-step flow
    RENDER StepIndicator(totalSteps=5, activeStep=currentStep)

    // Main Content Area
    CONTAINER MainContent:
        RENDER children