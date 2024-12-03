<script lang="ts">
	import { isFilled, type Content } from '@prismicio/client';
	import { PrismicImage } from '@prismicio/svelte';

	import PrismicRichText from '$lib/components/PrismicRichText.svelte';

	export let card: Content.ImageCardsSliceCardFullImagePrimaryCardsItem;
	// console.log('card', card);
</script>

<li
	class={`grid gap-8 w-[${card.fullimage.dimensions?.width}] h-[${card.fullimage.dimensions?.height}] overflow-hidden rounded-xl relative`}
>
	<PrismicImage
		field={card.fullimage}
		class="object-cover"
		width={card.fullimage.dimensions?.width}
		height={card.fullimage.dimensions?.height}
	/>

	<div
		class="leading-relaxed text-xl text-white absolute w-full bottom-0 text-center px-6 py-4 bg-gradient-to-b from-white/30 to-gray-800 drop-shadow-[2px_2px_var(--tw-shadow-color)] shadow-gray-800"
	>
		<PrismicRichText field={card.text} />
	</div>
</li>
