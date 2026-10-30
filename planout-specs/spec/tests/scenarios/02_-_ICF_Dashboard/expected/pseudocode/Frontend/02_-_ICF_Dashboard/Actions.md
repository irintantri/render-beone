Component Actions(row):
  Render:
    If row.status == "Approved":
      <IconView onClick={navigateToPreview(row.id)} />
      <IconOpen onClick={navigateToPreview(row.id)} />
    Else If row.status == "Draft" OR "In Review":
      <IconView onClick={navigateToPreview(row.id)} />
      <IconOpen onClick={navigateToEdit(row.id)} />
    Else:
      <span>—</span>

  Action navigateToPreview(id):
    // Transition to 07 - ICF Creation - Preview (01e2b39a-7c2a-4f69-8680-1c4ea18abe07) via /preview/{id}

  Action navigateToEdit(id):
    // Transition to 05 - ICF Creation - Edit and Refine (f8255b5b-e0d3-43aa-8948-4632c1a7a23a)

// Notes covered:
// - View icon navigates to preview page
// - Open icon navigates to edit page for drafts/in-review
// - Open icon navigates to /preview/{id} for approved documents
// - Non-actionable rows show a dash