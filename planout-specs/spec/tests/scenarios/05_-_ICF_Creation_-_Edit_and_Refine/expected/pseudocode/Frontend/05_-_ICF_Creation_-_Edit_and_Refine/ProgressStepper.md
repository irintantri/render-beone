/**
 * Node: Progress Stepper (id: 01d48ed8-ec1d-41a0-83b1-f26ac6bfcb2a)
 * Description: Visual indicator of the ICF creation workflow stages.
 * Asset: assets/ecabe235-1192-4f14-bb90-3389f1275208.svg
 */

interface ProgressStepperProps {
  currentStep: number; // 1: Setup, 2: Generate, 3: Edit/Refine, 4: Review
  totalSteps: number; // Fixed at 4
}

export const ProgressStepper = ({ currentStep, totalSteps = 4 }: ProgressStepperProps) => {
  const steps = ["Setup", "Generate", "Edit & Refine", "Review"];

  return (
    <nav aria-label="ICF Creation Progress">
      <ol>
        {steps.map((label, index) => {
          const stepNumber = index + 1;
          const isCompleted = stepNumber < currentStep;
          const isCurrent = stepNumber === currentStep;

          return (
            <li key={label} className={isCurrent ? "active" : isCompleted ? "completed" : "pending"}>
              <span className="step-indicator">{isCompleted ? "✓" : stepNumber}</span>
              <span className="step-label">{label}</span>
            </li>
          );
        })}
      </ol>
    </nav>
  );
};

/**
 * Logic:
 * - Happy Path: Renders 4 steps. Highlights current step based on state.
 * - Validation: None (read-only display component).
 * - Empty State: N/A (always initialized with 4 steps).
 * - Side Effects: None.
 */

// Notes covered:
// - Visual indicator of the ICF creation workflow stages.