<script lang="ts">
	import type { Content } from '@prismicio/client';
	import * as prismicR from '@prismicio/richtext';
	import clsx from 'clsx';
	import Heading from '$lib/components/Heading.svelte';
	import Bounded from '$lib/components/Bounded.svelte';
	import PrismicRichText from '$lib/components/PrismicRichText.svelte';
	import { PrismicText } from '@prismicio/svelte';

	export let slice: Content.TextSlice;
</script>

{#if slice.variation !== 'headerOnly'}
	<section
		class="grid grid-cols-1 gap-4 items-center md:flex max-w-7xl mx-auto h-full max-h-[1200px] w-full max-md:max-w-full px-4 py-6 md:py-10 lg:py-14 prose-p:text-base prose-h2:text-3xl prose-h3:text-2xl prose-h3:font-semibold prose-h4:text-xl"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class={clsx(slice.variation === 'twoColumns' && 'md:columns-2 md:gap-6')}>
			<PrismicRichText field={slice.primary.text} />
		</div>
	</section>
{/if}
{#if slice.variation === 'headerOnly'}
	<div
		class="bg-white leading-relaxed mt-8 text-center"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<Heading
			as="h2"
			size="4xl"
			id={prismicR
				.asText(slice.primary.text)
				.toLowerCase()
				.replace(/[^\w\s-]/g, '')
				.replace(/[\s_-]+/g, '-')
				.replace(/(^-|-$)/g, '')}
		>
			<PrismicText field={slice.primary.text} />
		</Heading>
	</div>
{/if}
