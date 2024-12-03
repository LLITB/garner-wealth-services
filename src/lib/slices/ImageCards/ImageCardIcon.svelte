<script lang="ts">
	import { isFilled, type Content } from '@prismicio/client';
	import { PrismicImage, PrismicLink } from '@prismicio/svelte';
	import * as prismicR from '@prismicio/richtext';
	import PrismicRichText from '$lib/components/PrismicRichText.svelte';
	import { PrismicText } from '@prismicio/svelte';
	import Heading from '$lib/components/Heading.svelte';

	export let card: Content.ImageCardsSliceCardWithIconPrimaryCardsItem;
</script>

<li class="flex flex-col gap-2 items-center pb-12 min-h-[315px] min-w-[240px] w-[232px]">
	{#if isFilled.image(card.image)}
		<div class="w-[50px] h-[50px]">
			<PrismicImage
				field={card.image}
				sizes="50px"
				class="object-contain w-[50px] h-[50px] aspect-square mx-auto "
			/>
		</div>
	{/if}

	<div
		class="mt-5 w-full tracking-wider leading-none text-center prose prose-h3:text-sky-900 prose-h3:text-lg"
	>
		<Heading as="h5" size="xl">
			<PrismicText field={card.text} />
		</Heading>
	</div>
	{#if isFilled.richText(card.body)}
		<PrismicRichText field={card.body} />
	{/if}
	{#if isFilled.link(card.buttonLink)}
		<div>
			<PrismicLink field={card.buttonLink} class="font-semibold">
				{card.buttonText || 'More Info'}
			</PrismicLink>
		</div>
	{/if}
</li>
