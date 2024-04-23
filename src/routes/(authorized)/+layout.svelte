<script lang="ts">
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import {jwtDecode} from 'jwt-decode';
	function isTokenValid(token: string) {
		try {
			const decodedToken = jwtDecode(token);
			const currentTime = Math.floor(Date.now() / 1000);
			if (decodedToken.exp && decodedToken.exp < currentTime) {
				console.log('Token has expired.');
				return false;
			}
			console.log('Token is valid.');
			return true;
		} catch (error) {
			console.error('Invalid token format.');
			return false;
		}
	}
	onMount(() => {
		const token = localStorage.getItem('token');
		if (!token || !isTokenValid(token)) {
			goto('/login');
		}
	});
</script>

<slot />
