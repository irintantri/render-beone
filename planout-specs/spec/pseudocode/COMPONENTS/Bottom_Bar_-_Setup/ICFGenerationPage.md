// Node: 04 - ICF Creation - Generate (id: a4c7e318-ef90-4130-bb36-73728bbf2bf6)
// Receives: schema from GenerateICFButton
function ICFGenerationPage({ schema }) {
    // Requirement: Real-time progress visualization of the AI generation pipeline.
    // Requirement: Displays six sequential checkpoints.
    const checkpoints = useGenerationPipeline(schema);

    useEffect(() => {
        if (checkpoints.isComplete) {
            // Requirement: Auto-navigates to the editor on completion.
            Navigation.replace('/icf-editor');
        }
    }, [checkpoints.isComplete]);

    return (
        <ProgressView steps={checkpoints} />
    );
}
// Notes covered:
// 1. Real-time progress visualization of AI generation pipeline.
// 2. Displays six sequential checkpoints.
// 3. Auto-navigates to the editor on completion.