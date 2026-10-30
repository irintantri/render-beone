// Node: Sorting (a769eaa2-0dac-4243-895a-f714c672e25d)
Component TableSorting:
  State sortKey: string | null
  State sortOrder: "asc" | "desc"
  
  Function onSort(field):
    If field == sortKey:
      sortOrder = (sortOrder == "asc") ? "desc" : "asc"
    Else:
      sortKey = field
      sortOrder = "asc"
    Call GET /api/protocol?sort_by={sortKey}&sort_order={sortOrder}
  
  Render:
    Headers: Clickable, display active indicator (▲/▼) if field == sortKey
// Notes covered: All column headers clickable, onSort(field) logic, toggle order, reset to asc on new field, active sort indicator.