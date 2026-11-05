// Node: Page Header (eeb59781-3936-49f7-adfa-9876a9eef4af)
// Asset: assets/9c78bc3d-f8fc-443c-a56d-64eda149905a.svg
const PageHeader = () => (
  <header>
    <h1>Consent IQ Dashboard</h1>
    <p>Manage and track Informed Consent Forms across all protocols</p>
    <button onClick={() => navigate('/setup')}>Create New Consent</button>
  </header>
);
// Notes covered: Title, Subtitle, Clicking "Create New Consent" button navigates to Setup page.

// Node: Global Navigation Header (9a4aeb94-1fa8-413d-b558-49bf51d025a1)
const GlobalNav = () => <nav>/* Global Navigation Elements */</nav>;

// Node: Statistics Cards (905e5c1d-85c0-449a-bc79-271e5276510e)
const StatsCards = ({ stats }) => (
  <div>
    <Card label="Total Consents" value={stats?.total ?? "—"} />
    <Card label="In Review" value={stats?.inReview ?? "—"} />
    <Card label="Approved" value={stats?.approved ?? "—"} />
  </div>
);
// Notes covered: Total Consents: Displays stats.total, In Review: Displays stats.inReview, Approved: Displays stats.approved, All default to "—" while loading.

// Node: Sortable Data Table (dc3a26aa-9207-442d-bf57-f961678a07ef)
const DataTable = ({ data }) => (
  <table>
    <thead>
      <tr>
        <th onClick={() => onSort('protocol_id')}>Protocol ID</th>
        <th onClick={() => onSort('version')}>Protocol Ver.</th> <!-- ORPHAN_FIELD: protocol_version -->
        <th onClick={() => onSort('name')}>Protocol Name</th>
        <th onClick={() => onSort('icf_name')}>ICF Name</th>
        <th onClick={() => onSort('icf_version')}>ICF Version</th>
        <th onClick={() => onSort('status')}>Status</th>
        <th onClick={() => onSort('last_modified')}>Last Modified</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      {data.map(row => (
        <tr key={row.id}>
          <td>{row.protocol_id}</td>
          <td>{row.version}</td>
          <td>{row.name}</td>
          <td>{row.icf_name}</td>
          <td>{row.icf_version}</td>
          <td><StatusBadge status={row.status} /></td>
          <td>{row.last_modified}</td>
          <td><ActionButtons row={row} /></td>
        </tr>
      ))}
    </tbody>
  </table>
);
// Notes covered: Column mapping for protocol_id, version, name, icf_name, icf_version, status, last_modified, Actions column, StatusBadge component.

// Node: Sorting (a769eaa2-0dac-4243-895a-f714c672e25d)
// Logic: Triggered by onSort(field) in DataTable
const onSort = (field) => {
  const newOrder = (sortKey === field && sortOrder === 'asc') ? 'desc' : 'asc';
  setSortKey(field);
  setSortOrder(newOrder);
  fetchData(`/api/protocol?sort_by=${field}&sort_order=${newOrder}`);
};
// Notes covered: All column headers are clickable, Clicking a header calls onSort(field), Same field toggles order, New field resets to ascending, Active sort indicator shown.

// Node: Actions (af34c83a-1d0b-479e-89e0-289d4ea91a5f)
const ActionButtons = ({ row }) => {
  if (!row.id) return <span>—</span>;
  return (
    <>
      <button onClick={() => navigate(`/preview/${row.id}`)}>View</button>
      <button onClick={() => {
        if (row.status === 'Approved') navigate(`/preview/${row.id}`);
        else navigate(`/edit/${row.id}`);
      }}>Open</button>
    </>
  );
};
// Notes covered: View icon navigates to preview, Open icon navigates to edit for drafts/in-review, Open icon navigates to /preview/{id} for approved, Non-actionable rows show a dash.