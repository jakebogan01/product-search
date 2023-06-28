<script>
	import { onMount } from 'svelte';
	import { env } from '$env/dynamic/public';
	import SearchBox from '../components/SearchBox.svelte';
	import Loader from '../components/Loader.svelte';
	import Nav from '../components/Nav.svelte';
	import Product from '../components/Product.svelte';
	import Footer from '../components/Footer.svelte';

	let showSearch = false;
	let searchInput = '';

	let apiLogic = {
		Products: [],
		currentPage: 1,
		pageCount: 20
	};

	onMount(async () => {
		fetchProducts();
	});

	// I also split the fetch into its own function so we can call it on the next and previous page buttons
	const fetchProducts = async (query = '') => {
		const response = await fetch(
			`https://api.searchspring.net/api/search/search.json?siteId=scmq7n&resultsFormat=native&resultsPerPage=${apiLogic.pageCount}&page=${apiLogic.currentPage}${query}`
		);
		const data = await response.json();

		if (response.ok) {
			apiLogic.Products[0] = data;
		} else {
			console.error(data.error);
		}
	};

	const handleSearchSubmit = (e) => {
		// check if search input is empty
		if (searchInput === '') {
			return;
		}
		apiLogic.currentPage = 1;
		fetchProducts(`&q=${searchInput}`);
		showSearch = false;
		// searchInput = '';
	};
</script>

<div class="bg-white">
	{#if showSearch}
		<SearchBox bind:showSearch bind:searchInput on:submit={handleSearchSubmit} />
	{/if}

	<Nav bind:showSearch />

	<main class="pb-24">
		<div class="px-4 py-16 text-center sm:px-6 lg:px-8">
			<h1 class="text-4xl font-bold tracking-tight text-gray-900">Most Popular</h1>
			<p class="mx-auto mt-4 max-w-xl text-base text-gray-500">
				Lookign for something new to add to your collection? We've got you covered.
			</p>
		</div>

		<!-- Product grid -->
		<section
			aria-labelledby="products-heading"
			class="mx-auto max-w-7xl overflow-hidden sm:px-6 lg:px-8"
		>
			<h2 id="products-heading" class="sr-only">Products</h2>
			{#if apiLogic.Products.length < 1}
				<Loader />
			{:else}
				<div
					class="-mx-px grid grid-cols-2 border-l border-gray-200 sm:mx-0 md:grid-cols-3 lg:grid-cols-4 border-t"
				>
					{#each apiLogic.Products[0].results as product (product.id)}
						<Product {product} />
					{:else}
						<p>There are no workouts</p>
					{/each}
				</div>
			{/if}
		</section>

		<!-- Pagination -->
		<nav
			aria-label="Pagination"
			class="mx-auto mt-6 flex max-w-7xl justify-between px-4 text-sm font-medium text-gray-700 sm:px-6 lg:px-8"
		>
			<div class="hidden sm:block">
				<p class="text-sm text-gray-700">
					Showing
					<span class="font-medium">{apiLogic.currentPage}</span>
					out of
					<span class="font-medium"
						>{apiLogic.Products[0]?.pagination?.totalPages.toLocaleString()}</span
					>
					pages
				</p>
			</div>
			<div class="flex flex-1 justify-between sm:justify-end">
				<button
					disabled={apiLogic.currentPage === 1}
					on:click={() => {
						apiLogic.currentPage = apiLogic.Products[0]?.pagination?.previousPage;
						if (searchInput !== '') {
							fetchProducts(`&q=${searchInput}`);
							return;
						}
						fetchProducts();
					}}
					type="button"
					class="disabled:opacity-50 relative inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus-visible:outline-offset-0"
				>
					Previous
				</button>
				<button
					disabled={apiLogic.currentPage === apiLogic.Products[0]?.pagination?.totalPages}
					on:click={() => {
						apiLogic.currentPage = apiLogic.Products[0]?.pagination?.nextPage;
						if (searchInput !== '') {
							fetchProducts(`&q=${searchInput}`);
							return;
						}
						fetchProducts();
					}}
					type="button"
					class="disabled:opacity-50 relative ml-3 inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus-visible:outline-offset-0"
				>
					Next
				</button>
			</div>
		</nav>
	</main>

	<Footer />
</div>
