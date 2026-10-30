// Asset: assets/9c78bc3d-f8fc-443c-a56d-64eda149905a.svg

Component ICFDashboard:
  State: stats = { total: null, inReview: null, approved: null }
  State: tableData = []
  State: sortConfig = { sort_by: null, sort_order: null }

  Effect: OnMount -> Call GET /api/stats -> stats = response.body
  Effect: OnMount -> Call GET /api/protocol -> tableData = response.body

  Render:
    <GlobalNavigationHeader />
    <PageHeader />
    <StatisticsCards stats={stats} />
    <SortableDataTable data={tableData} onSort={handleSort} />