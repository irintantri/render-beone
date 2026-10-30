// Frontend Layer: Renders the breadcrumb sub-bar.

interface BreadcrumbProps {
    showDashboard: boolean;
    label: string;
    protocolId?: string;
    icfName?: string;
    icfVersion?: string;
}

// Asset: assets/e368bbe4-c879-4b9e-8c43-c542dee64bfc.svg
export function BreadcrumbSubBar(props: BreadcrumbProps) {
    // Node: Breadcrumb sub-bar (e0e7bacf-cd43-4547-b546-782070237be2)
    // Requirement: Shows "Dashboard" link, "Consent Creation" label, protocol ID pill, ICF name crumb, and ICF version pill.
    // Requirement: Each element renders conditionally based on available props.

    return (
        <nav>
            {props.showDashboard && <Link to="/dashboard">Dashboard</Link>}
            <span>{props.label}</span>
            {props.protocolId && <Pill text={props.protocolId} />}
            {props.icfName && <span>{props.icfName}</span>}
            {props.icfVersion && <Pill text={props.icfVersion} />}
        </nav>
    );
}
// Notes covered: Shows "Dashboard" link, "Consent Creation" label, protocol ID pill, ICF name crumb, and ICF version pill, Each element renders conditionally based on available props.