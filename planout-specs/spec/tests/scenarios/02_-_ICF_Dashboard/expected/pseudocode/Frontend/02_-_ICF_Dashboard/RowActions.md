// Node: Actions (af34c83a-1d0b-479e-89e0-289d4ea91a5f)
Component RowActions(row):
  Render:
    If row.status == "Approved":
      Button "View": Navigate to "07 - ICF Creation - Preview" (01e2b39a-7c2a-4f69-8680-1c4ea18abe07)
      Button "Open": Navigate to "/preview/{row.id}"
    Else if row.status == "Draft" OR "In Review":
      Button "View": Navigate to "07 - ICF Creation - Preview" (01e2b39a-7c2a-4f69-8680-1c4ea18abe07)
      Button "Open": Navigate to "05 - ICF Creation - Edit and Refine" (f8255b5b-e0d3-43aa-8948-4632c1a7a23a)
    Else:
      Render "—"
// Notes covered: View icon navigation, Open icon navigation logic for drafts/in-review vs approved, non-actionable rows show dash.