<script lang="ts">
	import clsx from 'clsx';
	import type { Content } from '@prismicio/client';
	import Bounded from './Bounded.svelte';
	import Logo from './Logo.svelte';
	import { PrismicLink, PrismicText } from '@prismicio/svelte';

	/** @type {import("@prismicio/client").Content.SettingsDocument}*/

	export let settings: Content.SettingsDocument;
	export let navigation: Content.NavigationDocument;
</script>

<Bounded tag="footer" yPadding="sm" class="bg-[#F6F8FB]">
	<footer>
		<div class="my-8">
			<h4 class="text-2xl font-medium text-cyan-700 my-5">Disclosure</h4>
			<p class="text-base">
				Investment Advisory Services are offered through AdaptFirst Investments LLC, a registered
				investment adviser. Information presented is for educational purposes only and does not
				intend to make an offer or solicitation for the sale or purchase of any specific securities,
				investments, or investment strategies. Investments involve risk and unless otherwise stated,
				are not guaranteed. Commentary of any kind on this site is based on our own opinion and
				analysis, and not representative of future performance of any security or market.
				Personalized investment advice can only be rendered after engagement of the firm for
				services, execution of the required documentation, and receipt of required disclosures.
				Please contact the firm for further information. Information presented is not intended as
				tax or legal advice. Please consult legal or tax professionals for specific information
				regarding your individual situation.
			</p>
		</div>
		<nav class="flex flex-wrap items-center justify-between">
			<a href="/">
				<Logo />
				<span class="sr-only">{settings.data.siteTitle}</span>
			</a>
			<ul class="flex flex-wrap gap-6 md:gap-10">
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
	</footer>
</Bounded>
