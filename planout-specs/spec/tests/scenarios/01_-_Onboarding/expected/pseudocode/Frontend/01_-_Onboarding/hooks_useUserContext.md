import { useEffect, useState } from 'react';

export const useUserContext = () => {
  const [user, setUser] = useState(null);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    const fetchProfile = async () => {
      try {
        // API CALL: GET /users/me
        const response = await fetch('/users/me');
        const data = await response.json();
        setUser(data);
      } catch (err) {
        console.error("Failed to fetch user profile", err);
      } finally {
        setIsLoading(false);
      }
    };

    fetchProfile();
  }, []);

  return { user, isLoading };
};