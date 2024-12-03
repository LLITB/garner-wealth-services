<script lang="ts">
	import clsx from 'clsx';
	import type { Content } from '@prismicio/client';
	import { PrismicLink, PrismicText } from '@prismicio/svelte';
	import IconClose from './IconClose.svelte';
	import IconMenu from './IconMenu.svelte';
	import Bounded from './Bounded.svelte';
	import Logo from './Logo.svelte';
	export let settings: Content.SettingsDocument;
	export let navigation: Content.NavigationDocument;
	let isOpen = false;
	const toggleOpen = () => (isOpen = !isOpen);
	const close = () => (isOpen = false);
	function handleAnchorClick(event: { preventDefault: () => void; currentTarget: any }) {
		event.preventDefault();
		const link = event.currentTarget;
		const anchorId = new URL(link.href).hash.replace('#', '');
		const anchor = document.getElementById(anchorId);
		window.scrollTo({
			top: anchor!.offsetTop,
			behavior: 'smooth'
		});
	}
</script>

<Bounded tag="header" yPadding="xs" class=" border-b-2 border-cyan-700">
	<nav
		class="mx-auto flex max-w-6xl flex-col justify-between py-2 font-medium md:flex-row md:items-center"
	>
		<div class="flex items-center justify-between">
			<a href="/" on:click={close} class="z-50">
				<Logo />
				<span class="sr-only">{settings.data.siteTitle}</span>
			</a>
			<button
				type="button"
				class="block p-2 text-3xl text-black md:hidden"
				aria-expanded={isOpen}
				on:click={toggleOpen}
			>
				<IconMenu /></button
			>
		</div>
		<!-- Mobile Menu -->
		<div
			class={clsx(
				'fixed inset-0 z-40 flex flex-col items-end bg-slate-50 pr-4 pt-6 transition-transform duration-300 ease-in-out md:hidden',
				isOpen ? 'translate-x-0' : 'translate-x-[100%]'
			)}
		>
			<button
				aria-expanded={isOpen}
				type="button"
				class="block p-2 text-3xl text-black md:hidden"
				on:click={toggleOpen}
			>
				<IconClose />
			</button>
			<ul class="grid justify-items-end gap-4">
				{#each navigation.data?.links as item}
					<li
						class={clsx(
							item.external === true
								? 'relative inline-flex h-fit w-fit rounded-full border border-cyan-900/20 bg-cyan-200/10 px-4 py-2 text-cyan-700 outline-none ring-orange-700 transition-colors after:absolute after:inset-0 after:-z-10 after:animate-pulse after:rounded-full after:bg-orange-100 after:bg-opacity-0 after:blur-md after:transition-all after:duration-500 hover:border-orange-400/40 hover:text-orange-400 after:hover:bg-opacity-15 focus:ring-2 text-2xl'
								: 'py-4 px-2 hover:text-cyan-900 text-cyan-800 font-medium text-2xl'
						)}
					>
						<PrismicLink field={item.link} on:click={close}>
							<PrismicText field={item.label} />
						</PrismicLink>
					</li>
				{/each}
			</ul>
		</div>
		<!-- Desktop Menu -->
		<ul class="hidden md:flex flex-wrap items-center gap-1 md:gap-3">
			{#each navigation.data?.links as item}
				<li
					class={clsx(
						item.external === true
							? 'relative inline-flex h-fit w-fit rounded-full border border-cyan-900/20 bg-cyan-200/10 px-4 py-2 text-cyan-700 outline-none ring-orange-700 transition-colors after:absolute after:inset-0 after:-z-10 after:animate-pulse after:rounded-full after:bg-orange-100 after:bg-opacity-0 after:blur-md after:transition-all after:duration-500 hover:border-orange-400/40 hover:text-orange-400 after:hover:bg-opacity-15 focus:ring-2'
							: 'py-4 px-2 hover:text-cyan-900 text-cyan-800'
					)}
				>
					<PrismicLink field={item.link}>
						<PrismicText field={item.label} />
					</PrismicLink>
				</li>
			{/each}
			<li class="'py-4 px-2 hover:text-cyan-900 text-cyan-800'">
				<a href="/#key-benefits-of-working-with-us">Benefits</a>
			</li>
		</ul>
	</nav>
</Bounded>
