/**
 * Hook: useNavigation
 * Description: Centralized navigation logic to ensure consistent routing 
 * across the BeOne POC application.
 */

HOOK useNavigation() {
    IMPORT { useRouter } from 'framework/router';
    CONST router = useRouter();

    FUNCTION navigateTo(path: string) {
        // Logic to handle route transition
        // Can be extended for analytics tracking or transition animations
        router.push(path);
    }

    RETURN { navigateTo };
}