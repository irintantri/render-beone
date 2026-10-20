/**
 * Component: BottomBarGenerate
 * Description: A fixed bottom navigation bar for the Generate page.
 * Asset: assets/d4357674-d49a-4826-8fbb-8813a446b9c2.svg
 */

COMPONENT BottomBarGenerate(props: { jobId: string }) {
    IMPORT useNavigation from 'hooks/useNavigation';

    // Initialize navigation helper
    CONST { navigateTo } = useNavigation();

    // Handler for "Back to Setup"
    FUNCTION handleBackToSetup() {
        navigateTo('/create');
    }

    // Handler for "Skip"
    FUNCTION handleSkip() {
        // Navigates to edit mode for the current job context
        navigateTo(`/edit/${props.jobId}`);
    }

    RETURN (
        <Container style="fixed-bottom-bar">
            <GhostButton 
                label="Back to Setup" 
                onClick={handleBackToSetup} 
            />
            <GhostButton 
                label="Skip" 
                onClick={handleSkip} 
            />
        </Container>
    );
}