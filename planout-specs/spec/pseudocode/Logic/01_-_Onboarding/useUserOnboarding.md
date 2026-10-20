/**
 * Hook to manage the state of the welcome screen initialization.
 */
function useUserOnboarding() {
    const [user, setUser] = useState(null);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        async function initialize() {
            try {
                setLoading(true);
                const data = await api.get("/users/me");
                setUser(data);
            } catch (error) {
                handleError(error);
            } finally {
                setLoading(false);
            }
        }
        initialize();
    }, []);

    return { user, loading };
}