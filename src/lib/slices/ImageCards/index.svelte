<script lang="ts">
	import { onMount } from 'svelte';
	import * as prismicR from '@prismicio/richtext';
	import { isFilled, type Content } from '@prismicio/client';
	import { PrismicText } from '@prismicio/svelte';

	import Bounded from '$lib/components/Bounded.svelte';
	import ImageCard from './ImageCard.svelte';
	import Heading from '$lib/components/Heading.svelte';
	import CardNoImage from './CardNoImage.svelte';
	import ImageFullCard from './ImageFullCard.svelte';
	import ImageCardIcon from './ImageCardIcon.svelte';

	export let slice: Content.ImageCardsSlice;
	// onMount(()=>getFieldData(data))
</script>

{#if slice.variation === 'default'}
	<section
		class="bg-white"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class="grid gap-12">
			{#if isFilled.richText(slice.primary.heading)}
				<Heading
					as="h2"
					size="3xl"
					id={prismicR
						.asText(slice.primary.heading)
						.toLowerCase()
						.replace(/[^\w\s-]/g, '')
						.replace(/[\s_-]+/g, '-')
						.replace(/(^-|-$)/g, '')}
				>
					<PrismicText field={slice.primary.heading} getFieldData(slice.primary.heading) />
				</Heading>
			{/if}

			<ul class="grid grid-cols-1 items-start gap-8 md:grid-cols-2">
				{#each slice.primary.cards as card}
					<ImageCard {card} />
				{/each}
			</ul>
		</div>
	</section>
{/if}
{#if slice.variation === 'cardWithIcon'}
	<section
		class=" px-4 w-full bg-[#F6F8FB]"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class="grid gap-6 md:gap-12 py-5 md:py-10 max-w-7xl mx-auto">
			{#if isFilled.richText(slice.primary.heading)}
				<Heading
					as="h2"
					size="3xl"
					className="text-center"
					id={prismicR
						.asText(slice.primary.heading)
						.toLowerCase()
						.replace(/[^\w\s-]/g, '')
						.replace(/[\s_-]+/g, '-')
						.replace(/(^-|-$)/g, '')}
				>
					<PrismicText field={slice.primary.heading} />
				</Heading>
			{/if}

			<ul
				class="flex flex-wrap gap-4 lg:gap-14 md:items-start px-40 py-3 w-full md:px-5 md:max-w-4xl mx-auto"
			>
				{#each slice.primary.cards as card}
					<ImageCardIcon {card} />
				{/each}
			</ul>
		</div>
	</section>
{/if}
{#if slice.variation === 'cardFullImage'}
	<section
		class="bg-white max-w-7xl mx-auto px-8 pt-12 pb-6"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class="grid gap-12">
			{#if isFilled.richText(slice.primary.heading)}
				<Heading
					as="h2"
					size="3xl"
					className="text-center"
					id={prismicR
						.asText(slice.primary.heading)
						.toLowerCase()
						.replace(/[^\w\s-]/g, '')
						.replace(/[\s_-]+/g, '-')
						.replace(/(^-|-$)/g, '')}
				>
					<PrismicText field={slice.primary.heading} />
				</Heading>
			{/if}

			<ul class="grid grid-cols-1 md:grid-cols-4 gap-8 justify-center items-center mx-auto">
				{#each slice.primary.cards as card}
					<ImageFullCard {card} />
				{/each}
			</ul>
		</div>
	</section>
{/if}
{#if slice.variation === 'cardNoImageOrButton'}
	<section
		class="flex flex-col gap-4 py-6 lg:py-12 md:justify-around w-full max-md:max-w-full bg-[#156F89]"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class="grid gap-12 mx-auto max-w-7xl bg-[#156F89]">
			{#if isFilled.richText(slice.primary.heading)}
				<!-- <Heading className="text-white leading-relaxed" as="h3" size="3xl"
				
				>
					<PrismicText field={slice.primary.heading} />
				</Heading> -->
				<!-- {slice.primary.heading[0].text} -->
				<Heading
					as="h2"
					size="3xl"
					id={prismicR
						.asText(slice.primary.heading)
						.toLowerCase()
						.replace(/[^\w\s-]/g, '')
						.replace(/[\s_-]+/g, '-')
						.replace(/(^-|-$)/g, '')}
					className="text-white text-center"
				>
					<PrismicText field={slice.primary.heading} />
				</Heading>
			{/if}

			<ul class="flex flex-wrap gap-8 mx-auto justify-center">
				{#each slice.primary.cards as card}
					<CardNoImage {card} />
				{/each}
			</ul>
		</div>
	</section>
{/if}
