Component SortableDataTable(data, onSort):
  Render:
    Table:
      Header:
        Cell("Protocol ID", onClick: () => onSort("protocol_id"))
        Cell("Protocol Ver.", onClick: () => onSort("version")) <!-- ORPHAN_FIELD: protocol_version -->
        Cell("Protocol Name", onClick: () => onSort("name"))
        Cell("ICF Name", onClick: () => onSort("icf_name"))
        Cell("ICF Version", onClick: () => onSort("icf_version"))
        Cell("Status", onClick: () => onSort("status"))
        Cell("Last Modified", onClick: () => onSort("last_modified"))
        Cell("Actions")
      Rows:
        For row in data:
          <StatusBadge status={row.status} />
          <Actions row={row} />