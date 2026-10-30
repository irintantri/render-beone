Component StatisticsCards(stats):
  Render:
    Card("Total Consents", stats.total ?? "—")
    Card("In Review", stats.inReview ?? "—")
    Card("Approved", stats.approved ?? "—")

// Notes covered:
// - Title: "Consent IQ Dashboard"
// - Subtitle: "Manage and track Informed Consent Forms across all protocols"
// - Clicking "Create New Consent" button navigates to Setup page
// - Display statistic cards as follows: Total Consents, In Review, Approved
// - All default to "—" while loading