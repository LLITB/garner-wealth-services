<script lang="ts">
	import clsx from 'clsx';
	import type { Content } from '@prismicio/client';
	import { PrismicLink, PrismicText } from '@prismicio/svelte';

	import Bounded from './Bounded.svelte';
	import Logo from './Logo.svelte';
	export let settings: Content.SettingsDocument;
	export let navigation: Content.NavigationDocument;
</script>

<Bounded tag="header" yPadding="xs" class=" border-b-2 border-cyan-700">
	<div class="flex flex-wrap items-center justify-between gap-x-6 gap-y-3 leading-none">
		<a href="/">
			<Logo />
			<span class="sr-only">{settings.data.siteTitle}</span>
		</a>
		<nav class="flex flex-wrap gap-4 items-center">
			<ul class="flex flex-wrap gap-1 md:gap-3">
				<li class="py-4 px-2 hover:text-cyan-900 text-cyan-800">
					<a href="#benefits">benefits</a>
				</li>
				<li class="py-4 px-2 hover:text-cyan-900 text-cyan-800">
					<a href="#services">Services</a>
				</li>
				<li class="py-4 px-2 hover:text-cyan-900 text-cyan-800">
					<a href="#expertise">Areas of Expertise</a>
				</li>
				<li class="py-4 px-2 hover:text-cyan-900 text-cyan-800"><a href="#contact">Contact</a></li>
			</ul>
			<ul class="flex flex-wrap gap-1 md:gap-3">
				{#each navigation.data?.links as item}
					<li
						class={clsx(
							'relative inline-flex h-fit w-fit rounded-full border border-cyan-900/20 bg-cyan-200/10 px-4 py-2 text-cyan-700 outline-none ring-orange-700 transition-colors after:absolute after:inset-0 after:-z-10 after:animate-pulse after:rounded-full after:bg-orange-100 after:bg-opacity-0 after:blur-md after:transition-all after:duration-500 hover:border-orange-400/40 hover:text-orange-400 after:hover:bg-opacity-15 focus:ring-2'
						)}
					>
						<PrismicLink field={item.link}>
							<PrismicText field={item.label} />
						</PrismicLink>
					</li>
				{/each}
			</ul>
		</nav>
	</div>
</Bounded>
