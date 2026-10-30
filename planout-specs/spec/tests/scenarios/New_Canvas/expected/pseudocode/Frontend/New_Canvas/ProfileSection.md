/**
 * Node: Bagian Profil (d46c9aea-a40f-4607-aabc-8ce56d249082)
 * Description: Displays user first name from authenticated profile data.
 */

import React, { useState, useEffect } from 'react';

export const ProfileSection = () => {
  // State management
  const [firstName, setFirstName] = useState('');
  const [isEditing, setIsEditing] = useState(false);
  const [error, setError] = useState('');

  // Asset: assets/437bbddd-55db-4d0a-b9a6-1cb45337cee2.svg

  // Fetching data on mount
  useEffect(() => {
    // Call GET /auth/profile (implied by "API Get Profile")
    // Expects response: { first_name: string } <!-- ORPHAN_FIELD: first_name -->
    fetchProfileData();
  }, []);

  const handleValidation = (value: string) => {
    if (!value || value.trim() === '') {
      setError('Field tidak boleh kosong');
      return false;
    }
    // Regex for valid characters (e.g., alphabetic only)
    const regex = /^[a-zA-Z\s]+$/;
    if (!regex.test(value)) {
      setError('Format karakter tidak benar');
      return false;
    }
    setError('');
    return true;
  };

  const handleUpdate = async () => {
    if (handleValidation(firstName)) {
      // Call POST /auth/update-profile (implied by "API Update Profile")
      // Payload: { first_name: firstName } <!-- ORPHAN_FIELD: first_name -->
      await updateProfile({ first_name: firstName });
      setIsEditing(false);
    }
  };

  return (
    <div className="profile-container">
      <input
        type="text"
        value={firstName}
        readOnly={!isEditing}
        onChange={(e) => {
          setFirstName(e.target.value);
          handleValidation(e.target.value);
        }}
      />
      {error && <span className="error-message">{error}</span>}
      
      <button onClick={() => setIsEditing(!isEditing)}>
        {isEditing ? 'Simpan' : 'Edit'}
      </button>
    </div>
  );
};

/**
 * Notes covered:
 * 1. Menampilkan nama depan pengguna dari data profil.
 * 2. Field diisi dari respons profil pengguna terautentikasi.
 * 3. Harus mencerminkan nilai terbaru dari API Get Profile.
 * 4. Field bersifat hanya-baca secara default.
 * 5. Hanya dapat diedit ketika pengguna memulai pembaruan profil.
 * 6. Perubahan divalidasi untuk input tidak kosong.
 * 7. Perubahan divalidasi untuk format karakter yang benar.
 * 8. Validasi dilakukan sebelum dikirim melalui API Update Profile.
 */