<script>
	import { onMount } from 'svelte';
	import SearchProducts from '../stores/searchProducts';
	export let showSearch;
	let searchInput = '';

	onMount(() => {
		SearchProducts.set([]);
	});

	const fetchSearchProducts = async (query = '') => {
		const response = await fetch(
			`https://api.searchspring.net/api/search/search.json?siteId=scmq7n&resultsFormat=native&page=1${query}`
		);
		const data = await response.json();

		if (response.ok) {
			SearchProducts.set([data]);
		}
	};

	const handleSearchSubmit = (e) => {
		// check if search input is empty
		if (searchInput === '') {
			return;
		}
		fetchSearchProducts(`&q=${searchInput}`);
	};
</script>

<div
	class="fixed inset-0 z-50 flex items-start justify-center pt-16 sm:pt-24"
	id="headlessui-dialog-530"
	role="dialog"
	aria-modal="true"
	data-headlessui-state="open"
	on:keydown={() => {}}
	on:click|self={() => (showSearch = false)}
>
	<div
		class="fixed inset-0 bg-slate-900/25 backdrop-blur transition-opacity opacity-100"
		on:keydown={() => {}}
		on:click|self={() => (showSearch = false)}
	/>
	<div
		class="relative w-full max-w-lg transform px-4 transition-all opacity-100 scale-100"
		on:keydown={() => {}}
		on:click|self={() => (showSearch = false)}
	>
		<div
			class="overflow-hidden rounded-lg bg-white shadow-md"
			id="headlessui-dialog-panel-531"
			data-headlessui-state="open"
		>
			<form
				on:submit|preventDefault={handleSearchSubmit}
				class="relative flex items-center justify-between shadow-sm"
			>
				<input
					class="block w-full appearance-none bg-transparent py-4 pl-4 pr-12 text-base text-slate-900 outline-none border-0 border-none placeholder:text-slate-600 focus:outline-none sm:text-sm sm:leading-6 focus-visible"
					placeholder="Find anything..."
					aria-label="Search components"
					id="headlessui-combobox-input-532"
					role="combobox"
					type="text"
					aria-expanded="true"
					aria-autocomplete="list"
					data-headlessui-state="open"
					bind:value={searchInput}
					tabindex="0"
					style="caret-color: rgb(107, 114, 128);"
					data-focus-visible-added=""
					aria-controls="headlessui-combobox-options-533"
				/>
				<button type="submit"
					><svg
						class="cursor-pointer absolute right-4 top-4 h-6 w-6 fill-slate-400"
						xmlns="http://www.w3.org/2000/svg"
						><path
							d="M20.47 21.53a.75.75 0 1 0 1.06-1.06l-1.06 1.06Zm-9.97-4.28a6.75 6.75 0 0 1-6.75-6.75h-1.5a8.25 8.25 0 0 0 8.25 8.25v-1.5ZM3.75 10.5a6.75 6.75 0 0 1 6.75-6.75v-1.5a8.25 8.25 0 0 0-8.25 8.25h1.5Zm6.75-6.75a6.75 6.75 0 0 1 6.75 6.75h1.5a8.25 8.25 0 0 0-8.25-8.25v1.5Zm11.03 16.72-5.196-5.197-1.061 1.06 5.197 5.197 1.06-1.06Zm-4.28-9.97c0 1.864-.755 3.55-1.977 4.773l1.06 1.06A8.226 8.226 0 0 0 18.75 10.5h-1.5Zm-1.977 4.773A6.727 6.727 0 0 1 10.5 17.25v1.5a8.226 8.226 0 0 0 5.834-2.416l-1.061-1.061Z"
						/></svg
					></button
				>
			</form>
			<ul
				class="max-h-[18.375rem] divide-y divide-slate-200 overflow-y-auto rounded-b-lg border-t border-slate-200 text-sm leading-6"
				role="listbox"
				id="headlessui-combobox-options-533"
				data-headlessui-state="open"
			>
				{#if $SearchProducts.length < 1}
					<p />
				{:else}
					{#each $SearchProducts[0].results as product (product.id)}
						<li
							class="flex items-center justify-between p-4 cursor-pointer opacity-60 hover:opacity-100"
							id="headlessui-combobox-option-534"
							role="option"
							tabindex="-1"
							aria-selected="false"
							data-headlessui-state=""
						>
							<img
								src={product.thumbnailImageUrl}
								alt={product.name}
								class="w-[40px] object-cover object-center rounded-md"
							/>
							<span
								class="flex items-center ml-4 text-right whitespace-nowrap font-semibold text-slate-900"
							>
								<span class="block truncate max-w-[300px]">{product.name}</span>
							</span>
						</li>
					{:else}
						<p>There are no workouts</p>
					{/each}
				{/if}
			</ul>
		</div>
	</div>
</div>
