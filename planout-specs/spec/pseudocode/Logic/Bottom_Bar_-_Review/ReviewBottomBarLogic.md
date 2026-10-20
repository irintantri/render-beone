/**
 * Logic for the Bottom Action Bar on the 06 - Review page.
 * This component manages the state of the "Submit for Approval" action
 * and handles the transition to the 07 - ICF Creation - Preview page.
 */

function useReviewBottomBar(documentId: string) {
  // State to track open comments count for the button label
  const [openCommentsCount, setOpenCommentsCount] = useState<number>(0);
  const [isSubmitting, setIsSubmitting] = useState<boolean>(false);

  // Fetch current document status and comment metadata
  // <!-- MISSING_FIELD: DOCUMENT.open_comments_count -->
  // <!-- MISSING_FIELD: DOCUMENT.status -->

  const getButtonLabel = () => {
    if (openCommentsCount > 0) {
      return `Submit for Approval (${openCommentsCount} open)`;
    }
    return "Submit for Approval";
  };

  const handleSubmitForApproval = async () => {
    setIsSubmitting(true);
    
    try {
      // Trigger the approval workflow
      // API: POST /api/documents/{documentId}/submit-approval
      const response = await api.post(`/api/documents/${documentId}/submit-approval`);

      if (response.status === 200) {
        // On success, navigate to the Preview page
        navigateTo("07 - ICF Creation - Preview");
      }
    } catch (error) {
      handleError(error);
    } finally {
      setIsSubmitting(false);
    }
  };

  return {
    buttonLabel: getButtonLabel(),
    isSubmitting,
    handleSubmitForApproval,
    canSubmit: openCommentsCount === 0 // Logic gate: only allow if no open comments
  };
}