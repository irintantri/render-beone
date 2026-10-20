// Main component rendering the progress UI
import { useGenerationPolling } from './useGenerationPolling';

const STEPS = [
  "Parsing protocol data",
  "Loading reference documents",
  "Applying regulatory templates",
  "Generating consent sections",
  "Running compliance checks",
  "Finalizing document"
];

export const GenerationVisualization = ({ jobId, protocolId }) => {
  const { progress, step_label } = useGenerationPolling(jobId);
  
  // Calculate current step index based on progress (0-100 mapped to 0-6)
  const currentStepIndex = Math.floor((progress / 100) * STEPS.length);
  const etaSeconds = Math.max(0, Math.round((100 - progress) * 3));
  const etaFormatted = `${Math.floor(etaSeconds / 60).toString().padStart(2, '0')}:${(etaSeconds % 60).toString().padStart(2, '0')}`;

  return (
    <div className="generation-container">
      <h1>Generating Consent Form</h1>
      <p>Creating ICF for <strong>{protocolId}</strong></p>
      
      {/* ETA Display */}
      <div className="eta-display">
        <Icon name="clock" />
        <span>{etaFormatted}</span>
      </div>

      {/* Progress Bar */}
      <div className="progress-track">
        <div className="progress-fill" style={{ width: `${progress}%` }} />
      </div>

      {/* Checklist */}
      <ul className="checklist">
        {STEPS.map((label, index) => {
          const isDone = index < currentStepIndex;
          const isActive = index === currentStepIndex && progress < 100;
          
          return (
            <li key={index} className={isDone ? 'done' : isActive ? 'active' : 'pending'}>
              {isDone && <Icon name="check-green" />}
              {isActive && <Spinner />}
              <span>{label}</span>
              {isActive && <small>{step_label}</small>} <!-- ORPHAN_FIELD: step_label -->
            </li>
          );
        })}
      </ul>

      <footer>
        {progress}% complete — please do not close this window
      </footer>
    </div>
  );
};

Asset: assets/0f440293-ce09-4cbb-8748-0f9854854032.svg