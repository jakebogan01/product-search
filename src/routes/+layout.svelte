<script>
	import '../app.css';
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';
	import { browser } from '$app/environment';

	if (browser) {
		const Products = writable([]);
		setContext('Products', Products);
	}
</script>

<slot />
