<script>
	export let product;
</script>

<div class="group relative border-b border-r border-gray-200 p-4 sm:p-6">
	<div class="aspect-h-1 aspect-w-1 overflow-hidden rounded-lg bg-gray-200 group-hover:opacity-75">
		<img
			src={product?.thumbnailImageUrl || product?.imageUrl}
			alt={product.name}
			class="h-full w-full object-cover object-center"
		/>
	</div>
	<div class="pb-4 pt-10 text-center">
		<h3 class="text-sm font-medium text-gray-900">
			<a href="#" class="block truncate">
				<span aria-hidden="true" class="absolute inset-0" />
				{product.name}
			</a>
		</h3>
		<div class="mt-3 flex flex-col items-center">
			<p class="sr-only">5 out of 5 stars</p>
			<div class="flex items-center">
				<svg
					class="text-yellow-400 h-5 w-5 flex-shrink-0"
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						fill-rule="evenodd"
						d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
						clip-rule="evenodd"
					/>
				</svg>
				<svg
					class="text-yellow-400 h-5 w-5 flex-shrink-0"
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						fill-rule="evenodd"
						d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
						clip-rule="evenodd"
					/>
				</svg>
				<svg
					class="text-yellow-400 h-5 w-5 flex-shrink-0"
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						fill-rule="evenodd"
						d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
						clip-rule="evenodd"
					/>
				</svg>
				<svg
					class="text-yellow-400 h-5 w-5 flex-shrink-0"
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						fill-rule="evenodd"
						d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
						clip-rule="evenodd"
					/>
				</svg>
				<svg
					class="text-yellow-400 h-5 w-5 flex-shrink-0"
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						fill-rule="evenodd"
						d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
						clip-rule="evenodd"
					/>
				</svg>
			</div>
			<p class="mt-1 text-sm text-gray-500">{product.ratingCount} reviews</p>
		</div>
		{#if product?.msrp > product?.price}
			<div class="flex items-center space-x-4 justify-center">
				<p class="mt-4 text-base font-medium text-gray-900">${product?.msrp}</p>
				<p class="mt-4 text-base font-medium text-gray-900 relative">
					<span class="absolute -translate-y-1">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="2.5"
							stroke="currentColor"
							class="w-8 h-8 text-red-500"
						>
							<path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
						</svg>
					</span>
					${product?.price}
				</p>
			</div>
		{:else}
			<p class="mt-4 text-base font-medium text-gray-900">${product?.price}</p>
		{/if}
	</div>
</div>
