/**
 * Logic Node: GET /users/me (id: f358e2c8-39b1-4889-8db4-5528738310fe)
 * Interface: Cross-lane call to Logic swimlane.
 */

export const useUserContext = () => {
  const [state, setState] = useState({ user: null, taskCounts: null, isLoading: true, error: null });

  useEffect(() => {
    const fetchProfile = async () => {
      try {
        // API Call: GET /users/me
        const response = await fetch('/users/me', { method: 'GET' });
        const data = await response.json();
        
        setState({
          user: { 
            firstName: data.firstName, 
            lastName: data.lastName, 
            role: data.role, 
            secondaryRole: data.secondaryRole 
          },
          taskCounts: data.taskCounts, // <!-- ORPHAN_FIELD: taskCounts (inferred from response body) -->
          isLoading: false,
          error: null
        });
      } catch (err) {
        setState({ ...state, isLoading: false, error: err });
      }
    };
    fetchProfile();
  }, []);

  return state;
};