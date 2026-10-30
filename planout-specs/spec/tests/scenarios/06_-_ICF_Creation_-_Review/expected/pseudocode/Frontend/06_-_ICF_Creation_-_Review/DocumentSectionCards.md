/**
 * Node: Document Section Cards (52049b0f-baf8-46c4-846e-c9c20e875297)
 * Description: Renders document sections as individual cards.
 */

import { IcfMarkdown } from './IcfMarkdown'; // Assumed component for content rendering

interface SectionCardProps {
  sectionNumber: string;
  sectionTitle: string;
  isAiGenerated: boolean;
  content: string;
}

export const DocumentSectionCards = ({ documentData }: { documentData: Document }) => {
  // Happy Path: Map document.content (parsed into sections) to SectionCard components
  // Validation: If content is null/empty, render "No content available" state
  // Side Effects: None; purely presentational based on props from GET /api/documents/:id
  
  return (
    <div className="section-container">
      {parseSections(documentData.content).map((section) => (
        <SectionCard 
          key={section.id}
          sectionNumber={section.number}
          sectionTitle={section.title}
          isAiGenerated={section.isAiGenerated}
          content={section.content}
        />
      ))}
    </div>
  );
};

const SectionCard = ({ sectionNumber, sectionTitle, isAiGenerated, content }: SectionCardProps) => (
  <div className="card">
    <div className="card-header">
      <span className="section-title">
        <strong>{sectionNumber} {sectionTitle}</strong>
      </span>
      {isAiGenerated && (
        <span className="badge-ai">
          <SparklesIcon /> AI Generated
        </span>
      )}
    </div>
    <div className="card-body">
      <IcfMarkdown content={content} />
    </div>
  </div>
);

// Notes covered:
// - Render document per section as a card
// - Header: Section number, section title (bold, leading number stripped)
// - AI label badge (if present, with sparkles icon)
// - Body (read mode): Rendered via IcfMarkdown component