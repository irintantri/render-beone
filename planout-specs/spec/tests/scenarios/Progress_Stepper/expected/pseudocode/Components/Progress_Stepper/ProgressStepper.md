/**
 * Component: ProgressStepper
 * Asset: assets/61238dad-594f-4495-b090-7062b594f51f.svg
 */

interface Step {
  id: 'setup' | 'generate' | 'edit' | 'review' | 'preview';
  label: string;
  isClickable: boolean;
  route: string;
}

// Node: Functionality (id: 8e55a5d5-fecb-4e9f-a7ae-330bd606e0cf)
// Description: Horizontal five-step progress tracker rendered at the top of every creation screen.
// Steps: Setup, Generate, Edit & Refine, Review, Preview.
function ProgressStepper(currentStep: string, documentId: string | null) {
  const steps = [
    { id: 'setup', label: 'Setup', route: '/setup' },
    { id: 'generate', label: 'Generate', route: '/generate' },
    { id: 'edit', label: 'Edit & Refine', route: `/edit/${documentId}` },
    { id: 'review', label: 'Review', route: `/review/${documentId}` },
    { id: 'preview', label: 'Preview', route: `/preview/${documentId}` }
  ];

  // Happy Path: Render horizontal list of steps.
  // Empty State: If documentId is missing, steps requiring it are rendered as non-clickable.
  // Side Effects: None.
  return renderHorizontalList(steps.map(step => determineStepState(step, currentStep, documentId)));
}
// Notes covered: Horizontal five-step progress tracker, Rendered at top of creation screen, Steps: Setup, Generate, Edit & Refine, Review, Preview.

// Node: Navigation (id: 167b18c4-eb7a-484f-aecf-926ab3cc6bfe)
// Description: Completed and reachable steps are clickable buttons.
// Generate step is never directly navigable (transient).
// Edit, Review, and Preview steps require a `documentId` to be navigable.
function determineStepState(step, currentStep, documentId) {
  let isClickable = false;

  // Branch: "Generate" step
  if (step.id === 'generate') {
    isClickable = false; // Transient step rule
  } 
  // Branch: "Edit", "Review", "Preview" steps
  else if (['edit', 'review', 'preview'].includes(step.id)) {
    isClickable = documentId !== null; // Requires documentId
  } 
  // Branch: "Setup"
  else {
    isClickable = true;
  }

  return { ...step, isClickable };
}
// Notes covered: Completed and reachable steps are clickable, Generate step is never directly navigable, Edit/Review/Preview require documentId.

// Node: Step States (id: ccaa1dce-d29f-41e1-a001-ad2ca4da5d8b)
// Description: Each step renders as "done" (completed, shows check icon), "active" (current, highlighted), or "future" (grayed out).
function getStepVisualState(stepIndex, currentIndex) {
  // Branch: "done"
  if (stepIndex < currentIndex) {
    return { status: 'done', icon: 'check-mark', style: 'completed' };
  }
  // Branch: "active"
  else if (stepIndex === currentIndex) {
    return { status: 'active', icon: null, style: 'highlighted' };
  }
  // Branch: "future"
  else {
    return { status: 'future', icon: null, style: 'grayed-out' };
  }
}
// Notes covered: Each step renders as "done" (completed, shows check icon), "active" (current, highlighted), or "future" (grayed out).
// Ambiguity Flag: "Completed" status logic assumes linear progression; if non-linear jumps are allowed, "done" state may need to be explicitly passed via props rather than calculated by index.