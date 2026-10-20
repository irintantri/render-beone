// API definitions derived from the logic requirements

SERVICE SectionService
  
  // PATCH /api/sections/{id}
  // Updates the content of a specific section
  FUNCTION updateSection(id, payload)
    RETURN HTTP.PATCH(`/api/sections/${id}`, payload)

  // DELETE /api/sections/{id}
  // Removes a section from the document
  FUNCTION deleteSection(id)
    RETURN HTTP.DELETE(`/api/sections/${id}`)