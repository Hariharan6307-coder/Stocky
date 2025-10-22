<script>
	let searchQuery = $state('');
	let isDropdownVisible = $state(false);

	// Sample stock data
	const stocks = [
		{ name: 'NIFTY50', percentage: '+2.34', isPositive: true },
		{ name: 'S&P 500', percentage: '-1.18', isPositive: false },
    { name: 'NASDAQ', percentage: '+0.85', isPositive: true },
    { name: 'DOW JONES', percentage: '-0.45', isPositive: false }
	];

	function handleSearchFocus() {
		isDropdownVisible = true;
	}

	function handleClickOutside(event) {
		if (!event.target.closest('.search-container')) {
			isDropdownVisible = false;
		}
	}
</script>

<svelte:window on:click={handleClickOutside} />

<main class="p-5 max-w-4xl mx-auto">
	<div class="flex justify-center mt-10">
		<div class="relative w-full max-w-lg search-container">
			<div class="flex items-center bg-white border border-gray-300 rounded-full px-5 py-3 transition-all duration-300 ease-in-out">
				<img src="/icons/placeholder.png" alt="Search" class="w-5 h-5 mr-3 opacity-60" />
				<input
					type="text"
					bind:value={searchQuery}
					on:focus={handleSearchFocus}
					placeholder="Search for stocks, ETFs and more"
					class="flex-1 border-none outline-none text-base text-gray-800 bg-transparent placeholder-gray-500"
				/>
			</div>
			
			{#if isDropdownVisible}
				<div class="absolute top-full left-0 right-0 mt-2 bg-white border border-gray-200 rounded-lg z-10">
					{#each stocks as stock}
						<div class="flex items-center justify-between px-4 py-3 hover:bg-gray-50 cursor-pointer border-b border-gray-100 last:border-b-0">
							<span class="font-medium text-gray-800">{stock.name}</span>
							<span class="w-16 px-2 py-1 rounded-full text-sm font-semibold text-center {stock.isPositive ? 'bg-green-100 text-green-700' : 'bg-red-100 text-red-700'}">
								{stock.percentage}%
							</span>
						</div>
					{/each}
				</div>
			{/if}
		</div>
	</div>
</main>