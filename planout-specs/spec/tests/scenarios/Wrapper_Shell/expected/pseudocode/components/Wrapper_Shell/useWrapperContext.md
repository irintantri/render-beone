// Logic layer to manage the state of the wrapper shell
// This hook ensures the UI stays in sync with the current step and protocol data

FUNCTION useWrapperContext(initialStep, protocolData):
    DEFINE state currentStep AS initialStep
    DEFINE state protocolInfo AS protocolData

    FUNCTION updateStep(newStep):
        SET currentStep TO newStep

    RETURN {
        currentStep,
        protocolInfo,
        updateStep
    }