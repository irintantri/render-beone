import React, { useState, useEffect } from 'react';
import { useFetch } from './hooks/useFetch'; // Custom hook for API calls

/**
 * ICF Dashboard Component
 * Asset: assets/9c78bc3d-f8fc-443c-a56d-64eda149905a.svg
 */
export const ICFDashboard = () => {
  const [sortConfig, setSortConfig] = useState({ key: 'last_modified', order: 'desc' });
  const [searchQuery, setSearchQuery] = useState('');
  
  // Fetch Stats
  const { data: stats, loading: statsLoading } = useFetch('/api/stats');

  // Fetch Protocols (List or Search)
  const endpoint = searchQuery ? `/api/search?protocolName=${searchQuery}&ICFName=${searchQuery}` : `/api/protocol?sort_by=${sortConfig.key}&sort_order=${sortConfig.order}`;
  const { data: protocols, loading: listLoading } = useFetch(endpoint);

  const handleSort = (field) => {
    const order = (sortConfig.key === field && sortConfig.order === 'asc') ? 'desc' : 'asc';
    setSortConfig({ key: field, order });
  };

  return (
    <div className="dashboard-container">
      <header>
        <div className="logo-placeholder">BeOne Logo</div>
        <h1>Consent IQ Dashboard</h1>
        <p>Manage and track Informed Consent Forms across all protocols</p>
        <button onClick={() => navigate('/setup')}>Create New Consent</button>
      </header>

      <section className="stats-grid">
        <StatCard label="Total Consents" value={statsLoading ? '—' : stats?.total} />
        <StatCard label="In Review" value={statsLoading ? '—' : stats?.inReview} />
        <StatCard label="Approved" value={statsLoading ? '—' : stats?.approved} />
      </section>

      <input 
        type="text" 
        placeholder="Search protocols, ICF…" 
        onChange={(e) => setSearchQuery(e.target.value)} 
      />

      <table className="icf-table">
        <thead>
          <tr>
            <th onClick={() => handleSort('protocol_id')}>Protocol ID {sortConfig.key === 'protocol_id' && (sortConfig.order === 'asc' ? '▲' : '▼')}</th>
            <th onClick={() => handleSort('version')}>Protocol Ver.</th> <!-- ORPHAN_FIELD: protocol_version -->
            <th onClick={() => handleSort('name')}>Protocol Name</th> <!-- ORPHAN_FIELD: protocol_name -->
            <th onClick={() => handleSort('icf_name')}>ICF Name</th>
            <th onClick={() => handleSort('icf_version')}>ICF Version</th>
            <th>Status</th>
            <th onClick={() => handleSort('last_modified')}>Last Modified</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          {protocols?.map((item) => (
            <tr key={item.id}>
              <td>{item.protocol_id}</td>
              <td>{item.version}</td>
              <td>{item.name}</td>
              <td>{item.ICF?.name}</td>
              <td>{item.ICF?.version}</td>
              <td><StatusBadge status={item.status} /></td>
              <td>{item.last_modified}</td>
              <td>
                <ActionButtons 
                  status={item.status} 
                  id={item.id} 
                  icfId={item.ICF?.id} 
                />
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};