export const TaskSummary = ({ taskCounts }) => {
  return (
    <section>
      <p>
        <b>{taskCounts.draftsInProgress}</b> drafts in progress | 
        <b>{taskCounts.itemsAwaitingReview}</b> items awaiting your review
      </p>
    </section>
  );
};