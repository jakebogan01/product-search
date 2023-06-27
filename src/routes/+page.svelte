<script>
	import { onMount } from 'svelte';
	import Products from '../stores/products';
	import SearchBox from '../components/SearchBox.svelte';
	import Loader from '../components/Loader.svelte';
	import Product from '../components/Product.svelte';

	let menuOpen = true;
	let showSearch = false;
	let currentPage = 1;

	// I also split the fetch into its own function so we can call it on the next and previous page buttons
	// also, I split the fetch function into a separate function located in the SearchBox component so we can call it when the user submits the search form
	const fetchProducts = async () => {
		const response = await fetch(
			`https://api.searchspring.net/api/search/search.json?siteId=scmq7n&resultsFormat=native&page=${currentPage}`
		);
		const data = await response.json();

		if (response.ok) {
			Products.set([data]);
		}
	};

	onMount(async () => {
		fetchProducts();
	});
</script>

<div class="bg-white">
	{#if showSearch}
		<SearchBox bind:showSearch />
	{/if}

	{#if menuOpen}
		<div class="relative z-40 lg:hidden" role="dialog" aria-modal="true">
			<div class="fixed inset-0 bg-black bg-opacity-25" />

			<div class="fixed inset-0 z-40 flex">
				<div
					class="relative flex w-full max-w-xs flex-col overflow-y-auto bg-white pb-12 shadow-xl"
				>
					<div class="flex px-4 pb-2 pt-5">
						<button
							type="button"
							on:click={() => (menuOpen = false)}
							class="-m-2 inline-flex items-center justify-center rounded-md p-2 text-gray-400"
						>
							<span class="sr-only">Close menu</span>
							<svg
								class="h-6 w-6"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								aria-hidden="true"
							>
								<path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
							</svg>
						</button>
					</div>

					<!-- Links -->
					<div class="space-y-6 border-t border-gray-200 px-4 py-6">
						<div class="flow-root">
							<a href="#" class="-m-2 block p-2 font-medium text-gray-900">Company</a>
						</div>
						<div class="flow-root">
							<a href="#" class="-m-2 block p-2 font-medium text-gray-900">Stores</a>
						</div>
					</div>
				</div>
			</div>
		</div>
	{/if}

	<header class="relative bg-white">
		<nav aria-label="Top" class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<div class="border-b border-gray-200">
				<div class="flex h-16 items-center justify-between">
					<div class="flex flex-1 items-center lg:hidden">
						<!-- Mobile menu toggle, controls the 'mobileMenuOpen' state. -->
						<button
							type="button"
							on:click={() => (menuOpen = true)}
							class="-ml-2 rounded-md bg-white p-2 text-gray-400"
						>
							<span class="sr-only">Open menu</span>
							<svg
								class="h-6 w-6"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								aria-hidden="true"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
								/>
							</svg>
						</button>

						<button
							type="button"
							on:click={() => (showSearch = true)}
							class="ml-2 p-2 text-gray-400 hover:text-gray-500"
						>
							<span class="sr-only">Search</span>
							<svg
								class="h-6 w-6"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								aria-hidden="true"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
								/>
							</svg>
						</button>
					</div>

					<!-- Flyout menus -->
					<div class="hidden lg:block lg:flex-1 lg:self-stretch">
						<div class="flex h-full space-x-8">
							<div class="flex">
								<div class="relative flex">
									<!-- Item active: "text-indigo-600", Item inactive: "text-gray-700 hover:text-gray-800" -->
									<button
										type="button"
										class="text-gray-700 hover:text-gray-800 relative z-10 flex items-center justify-center text-sm font-medium transition-colors duration-200 ease-out"
										aria-expanded="false"
									>
										Women
										<!-- Open: "bg-indigo-600", Closed: "" -->
										<span
											class="absolute inset-x-0 bottom-0 h-0.5 transition-colors duration-200 ease-out sm:mt-5 sm:translate-y-px sm:transform"
											aria-hidden="true"
										/>
									</button>
								</div>
							</div>
							<div class="flex">
								<div class="relative flex">
									<!-- Item active: "text-indigo-600", Item inactive: "text-gray-700 hover:text-gray-800" -->
									<button
										type="button"
										class="text-gray-700 hover:text-gray-800 relative z-10 flex items-center justify-center text-sm font-medium transition-colors duration-200 ease-out"
										aria-expanded="false"
									>
										Men
										<!-- Open: "bg-indigo-600", Closed: "" -->
										<span
											class="absolute inset-x-0 bottom-0 h-0.5 transition-colors duration-200 ease-out sm:mt-5 sm:translate-y-px sm:transform"
											aria-hidden="true"
										/>
									</button>
								</div>
							</div>

							<a
								href="#"
								class="flex items-center text-sm font-medium text-gray-700 hover:text-gray-800"
								>Company</a
							>
							<a
								href="#"
								class="flex items-center text-sm font-medium text-gray-700 hover:text-gray-800"
								>Stores</a
							>
						</div>
					</div>

					<!-- Logo -->
					<a href="#" class="flex">
						<span class="sr-only">Your Company</span>
						<img class="h-8 w-auto rounded-md" src="/logo.jpeg" alt="" />
					</a>

					<div class="flex flex-1 items-center justify-end">
						<!-- Search -->
						<button
							type="button"
							on:click={() => (showSearch = true)}
							class="ml-6 hidden p-2 text-gray-400 hover:text-gray-500 lg:block"
						>
							<span class="sr-only">Search</span>
							<svg
								class="h-6 w-6"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								aria-hidden="true"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
								/>
							</svg>
						</button>

						<!-- Account -->
						<a href="#" class="p-2 text-gray-400 hover:text-gray-500 lg:ml-4">
							<span class="sr-only">Account</span>
							<svg
								class="h-6 w-6"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								aria-hidden="true"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M15.75 6a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.501 20.118a7.5 7.5 0 0114.998 0A17.933 17.933 0 0112 21.75c-2.676 0-5.216-.584-7.499-1.632z"
								/>
							</svg>
						</a>

						<!-- Cart -->
						<div class="ml-4 flow-root lg:ml-6">
							<a href="#" class="group -m-2 flex items-center p-2">
								<svg
									class="h-6 w-6 flex-shrink-0 text-gray-400 group-hover:text-gray-500"
									fill="none"
									viewBox="0 0 24 24"
									stroke-width="1.5"
									stroke="currentColor"
									aria-hidden="true"
								>
									<path
										stroke-linecap="round"
										stroke-linejoin="round"
										d="M15.75 10.5V6a3.75 3.75 0 10-7.5 0v4.5m11.356-1.993l1.263 12c.07.665-.45 1.243-1.119 1.243H4.25a1.125 1.125 0 01-1.12-1.243l1.264-12A1.125 1.125 0 015.513 7.5h12.974c.576 0 1.059.435 1.119 1.007zM8.625 10.5a.375.375 0 11-.75 0 .375.375 0 01.75 0zm7.5 0a.375.375 0 11-.75 0 .375.375 0 01.75 0z"
									/>
								</svg>
								<span class="ml-2 text-sm font-medium text-gray-700 group-hover:text-gray-800"
									>0</span
								>
								<span class="sr-only">items in cart, view bag</span>
							</a>
						</div>
					</div>
				</div>
			</div>
		</nav>
	</header>

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
			{#if $Products.length < 1}
				<Loader />
			{:else}
				<div
					class="-mx-px grid grid-cols-2 border-l border-gray-200 sm:mx-0 md:grid-cols-3 lg:grid-cols-4 border-t"
				>
					{#each $Products[0].results as product (product.id)}
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
					<span class="font-medium">{currentPage}</span>
					of
					<span class="font-medium">{$Products[0]?.pagination?.totalResults.toLocaleString()}</span>
					results
				</p>
			</div>
			<div class="flex flex-1 justify-between sm:justify-end">
				<button
					disabled={currentPage === 1}
					on:click={() => {
						currentPage = $Products[0]?.pagination?.previousPage;
						fetchProducts();
					}}
					type="button"
					class="disabled:opacity-50 relative inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 focus-visible:outline-offset-0"
				>
					Previous
				</button>
				<button
					disabled={currentPage === $Products[0]?.pagination?.totalPages}
					on:click={() => {
						currentPage = $Products[0]?.pagination?.nextPage;
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

	<footer aria-labelledby="footer-heading" class="bg-white">
		<h2 id="footer-heading" class="sr-only">Footer</h2>
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<div
				class="grid grid-cols-2 gap-8 border-t border-gray-200 py-20 sm:grid-cols-2 sm:gap-y-0 lg:grid-cols-4"
			>
				<div class="grid grid-cols-1 gap-y-10 lg:col-span-2 lg:grid-cols-2 lg:gap-x-8 lg:gap-y-0">
					<div>
						<h3 class="text-sm font-medium text-gray-900">Account</h3>
						<ul role="list" class="mt-6 space-y-6">
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Manage Account</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Saved Items</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Orders</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Redeem Gift card</a>
							</li>
						</ul>
					</div>
					<div>
						<h3 class="text-sm font-medium text-gray-900">Service</h3>
						<ul role="list" class="mt-6 space-y-6">
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Shipping &amp; Returns</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Warranty</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">FAQ</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Find a store</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Get in touch</a>
							</li>
						</ul>
					</div>
				</div>
				<div class="grid grid-cols-1 gap-y-10 lg:col-span-2 lg:grid-cols-2 lg:gap-x-8 lg:gap-y-0">
					<div>
						<h3 class="text-sm font-medium text-gray-900">Company</h3>
						<ul role="list" class="mt-6 space-y-6">
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Who we are</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Press</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Careers</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Terms &amp; Conditions</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Privacy</a>
							</li>
						</ul>
					</div>
					<div>
						<h3 class="text-sm font-medium text-gray-900">Connect</h3>
						<ul role="list" class="mt-6 space-y-6">
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Instagram</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Pinterest</a>
							</li>
							<li class="text-sm">
								<a href="#" class="text-gray-500 hover:text-gray-600">Twitter</a>
							</li>
						</ul>
					</div>
				</div>
			</div>

			<div class="border-t border-gray-100 py-10 sm:flex sm:items-center sm:justify-end">
				<p class="mt-6 text-center text-sm text-gray-500 sm:mt-0">&copy; 2021 Your Company, Inc.</p>
			</div>
		</div>
	</footer>
</div>
