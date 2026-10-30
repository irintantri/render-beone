Function handleSort(field):
  If sortConfig.sort_by == field:
    sortConfig.sort_order = (sortConfig.sort_order == "asc") ? "desc" : "asc"
  Else:
    sortConfig.sort_by = field
    sortConfig.sort_order = "asc"
  
  Call GET /api/protocol?sort_by={sortConfig.sort_by}&sort_order={sortConfig.sort_order}
  Update tableData with response

// Notes covered:
// - All column headers are clickable
// - Clicking a header calls onSort(field)
// - If same field, order toggles (asc ↔ desc)
// - If new field, sort order resets to ascending
// - Active sort indicator (▲/▼) shown next to current sort column