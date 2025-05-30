<svelte:options runes={true} />

<script>
	import { fade } from 'svelte/transition';
	import { page } from '$app/state';

	const tabs = [
		{
			name: 'Home',
			href: '/'
		},
		{
			name: 'About',
			href: '/about'
		},
		{
			name: 'Development',
			href: '/development'
		},
		{
			name: 'Projects',
			href: '/projects'
		},
		{
			name: 'AI Training',
			href: '/ai'
		}
	];
	let isMobileMenuOpen = $state(false);

	// Get current path to determine active link
	let currentPath = $derived(page.url.pathname);
</script>

<header class="absolute inset-x-0 top-0 z-50">
	<nav class="flex items-center justify-between p-6 lg:px-8" aria-label="Global">
		<div class="flex lg:flex-1">
			<a href="/" class="-m-1.5 p-1.5 flex items-center gap-3 group">
				<span class="sr-only">Roga Web Development</span>
				<img class="h-8 w-auto" src="/logo/favicon-32x32.png" alt="Roga Web Development Logo" />
				<span
					class="text-lg font-bold tracking-tight text-gray-600 transition-colors duration-200 group-hover:text-gray-800 relative"
				>
					Roga Web Development
					<span
						class="absolute -bottom-[5px] left-1/2 w-0 h-0.5 bg-gray-600 group-hover:w-full group-hover:left-0 transition-all duration-300 origin-center"
					></span>
				</span>
			</a>
		</div>
		<div class="flex lg:hidden">
			<button
				onclick={() => {
					isMobileMenuOpen = !isMobileMenuOpen;
				}}
				type="button"
				class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700"
			>
				<span class="sr-only">Open main menu</span>
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
		</div>
		<div class="hidden lg:flex lg:gap-x-12">
			{#each tabs as { name, href }}
				<a
					{href}
					class="text-sm font-semibold leading-6 text-gray-900 relative group"
					class:active={currentPath === href}
				>
					{name}
					<span
						class="absolute -bottom-[5px] left-0 h-0.5 bg-gray-600 transition-all duration-300
						{currentPath === href ? 'w-full' : 'w-0 group-hover:w-full'}"
					></span>
				</a>
			{/each}
		</div>
		<div class="hidden lg:flex lg:flex-1 lg:justify-end">
			<a href="/contact" class="text-sm font-semibold leading-6 text-gray-900 relative group">
				Contact <span aria-hidden="true">&rarr;</span>
				<span
					class="absolute -bottom-[5px] left-0 h-0.5 bg-gray-600 transition-all duration-300
					{currentPath === '/contact' ? 'w-full' : 'w-0 group-hover:w-full'}"
				></span>
			</a>
		</div>
	</nav>
	<!-- Mobile menu, show/hide based on menu open state. -->
	{#if isMobileMenuOpen}
		<div transition:fade class="lg:hidden" role="dialog" aria-modal="true">
			<!-- Background backdrop, show/hide based on slide-over state. -->
			<div class="fixed inset-0 z-50"></div>
			<div
				class="fixed inset-y-0 right-0 z-50 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10"
			>
				<div class="flex items-center justify-between">
					<a href="/" class="-m-1.5 p-1.5">
						<span class="sr-only">Roga Web Development</span>
						<img class="h-8 w-auto" src="/logo/favicon-32x32.png" alt="Roga Web Development Logo" />
					</a>
					<button
						onclick={() => {
							isMobileMenuOpen = !isMobileMenuOpen;
						}}
						type="button"
						class="-m-2.5 rounded-md p-2.5 text-gray-700"
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
				<div class="mt-6 flow-root">
					<div class="-my-6 divide-y divide-gray-500/10">
						<div class="space-y-2 py-6">
							{#each tabs as { name, href }}
								<a
									{href}
									onclick={() => (isMobileMenuOpen = false)}
									class="relative group -mx-3 block rounded-lg px-3 py-2 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50"
									class:active={currentPath === href}
								>
									{name}
									<span
										class="absolute bottom-1 left-3 h-0.5 bg-gray-600 transition-all duration-300
										{currentPath === href ? 'w-[calc(100%-24px)]' : 'w-0 group-hover:w-[calc(100%-24px)]'}"
									></span>
								</a>
							{/each}
						</div>
						<!-- <div class="py-6">
						<a
							href="#"
							class="-mx-3 block rounded-lg px-3 py-2.5 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-50"
							>Log in</a
						>
					</div> -->
					</div>
				</div>
			</div>
		</div>
	{/if}
</header>
