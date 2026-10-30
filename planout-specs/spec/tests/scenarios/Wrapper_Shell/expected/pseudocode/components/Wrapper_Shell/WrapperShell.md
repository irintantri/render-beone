// Frontend Layer: Main container component.

export function WrapperShell({ children, ...props }) {
    // Node: Props (a0f11c50-32e3-4939-b68e-88061fb729d3)
    // Interface: Receives data from useWrapperData hook.
    const data = useWrapperData(props.protocolId, props.icfName, props.icfVersion, props.currentStep);

    return (
        <div className="wrapper-shell">
            <TopBar />
            <BreadcrumbSubBar {...data.breadcrumbData} />
            <StepIndicator current={data.stepIndicator.currentStep} total={data.stepIndicator.totalSteps} />
            <main>{children}</main>
        </div>
    );
}
// Notes covered: (None - structural node for Props definition).