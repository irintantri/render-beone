// Node: Statistics Cards (3 cards) (905e5c1d-85c0-449a-bc79-271e5276510e)
Component StatisticsCards:
  State stats: { total: null, inReview: null, approved: null }
  OnMount: Call GET /api/stats
  Render:
    Card 1: "Total Consents" -> stats.total ?? "—"
    Card 2: "In Review" -> stats.inReview ?? "—"
    Card 3: "Approved" -> stats.approved ?? "—"
// Notes covered: Total Consents, In Review, Approved, default to "—" while loading.