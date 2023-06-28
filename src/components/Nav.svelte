<script>
	export let showSearch = false;
	let menuOpen = true;
</script>

{#if menuOpen}
	<div class="relative z-40 lg:hidden" role="dialog" aria-modal="true">
		<div class="fixed inset-0 bg-black bg-opacity-25" />

		<div class="fixed inset-0 z-40 flex">
			<div class="relative flex w-full max-w-xs flex-col overflow-y-auto bg-white pb-12 shadow-xl">
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
				<a href="/" class="flex">
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
							<span class="ml-2 text-sm font-medium text-gray-700 group-hover:text-gray-800">0</span
							>
							<span class="sr-only">items in cart, view bag</span>
						</a>
					</div>
				</div>
			</div>
		</div>
	</nav>
</header>
