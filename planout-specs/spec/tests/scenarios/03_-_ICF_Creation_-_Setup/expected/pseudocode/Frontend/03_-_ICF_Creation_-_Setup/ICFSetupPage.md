import React, { useState, useEffect } from 'react';
import { useProtocolSearch, useTemplates, useReferenceUpload } from './hooks/apiHooks';

/**
 * Asset: assets/dd46e12b-d629-4482-aabd-05f3d2b04e38.svg
 * Main container for the 3-column ICF Setup wizard.
 */
export const ICFSetupPage = () => {
  const [selectedProtocol, setSelectedProtocol] = useState(null);
  const [selectedTemplate, setSelectedTemplate] = useState('standard'); // Default ID
  const [attachedDocs, setAttachedDocs] = useState({ 'Investigation Brochure': null, 'Lab Manual': null });
  const [error, setError] = useState(null);

  const { protocols, loading: protocolsLoading } = useProtocolSearch();
  const { templates } = useTemplates();

  return (
    <div className="setup-wizard-container">
      <GlobalNavigationHeader />
      <ProgressStepper currentStep="Setup" />
      
      {error && <ErrorBanner message={error} onClose={() => setError(null)} />}

      <div className="wizard-grid">
        {/* Column 1: Protocol Selection */}
        <section>
          <SearchProtocol onSearch={(q) => /* Filter logic */} />
          {protocolsLoading ? <Spinner /> : (
            protocols.map(p => (
              <ProtocolCard 
                key={p.id} 
                data={p} 
                isSelected={selectedProtocol?.id === p.id}
                onClick={() => setSelectedProtocol(p)} 
              />
            ))
          )}
        </section>

        {/* Column 2: Reference Documents */}
        <section>
          <ReferenceDocuments 
            protocolId={selectedProtocol?.protocol_id}
            onAttach={(kind, doc) => setAttachedDocs(prev => ({ ...prev, [kind]: doc }))}
            onError={setError}
          />
        </section>

        {/* Column 3: Template Selection */}
        <section>
          {templates.map(t => (
            <TemplateCard 
              key={t.id} 
              data={t} 
              isSelected={selectedTemplate === t.id}
              onClick={() => setSelectedTemplate(t.id)}
            />
          ))}
        </section>
      </div>

      <BottomBarSetup 
        canProceed={!!selectedProtocol && !!selectedTemplate} 
        onLaunch={() => /* Trigger Generation */} 
      />
    </div>
  );
};