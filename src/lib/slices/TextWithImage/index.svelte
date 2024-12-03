<script lang="ts">
	import { isFilled, type Content } from '@prismicio/client';
	import { PrismicImage, PrismicText } from '@prismicio/svelte';

	import Bounded from '$lib/components/Bounded.svelte';

	import PrismicRichText from '$lib/components/PrismicRichText.svelte';

	export let slice: Content.TextWithImageSlice;

	// w-[${slice.primary.image.dimensions.width}]  h-[${slice.primary.image.dimensions.height}]
</script>

<section
	class="grid grid-cols-1 md:flex max-w-7xl gap-4 justify-items-center md:justify-around mx-auto my-5 lg:my-10 py-4 md:py-5 w-full max-md:max-w-full"
	data-slice-type={slice.slice_type}
	data-slice-variation={slice.variation}
>
	<div
		class="text-2xl text-center md:text-left max-w-3xl px-4 prose prose-a:py-2 prose-a:px-4 prose-a:border-2 prose-a:border-cyan-700 prose-a:rounded-md prose-a:text-base prose-a:no-underline"
	>
		<PrismicRichText field={slice.primary.text} />
	</div>
	<div class={`${slice.primary.direction_right ? 'md:order-first' : 'md:order-last'}`}>
		{#if isFilled.image(slice.primary.image)}
			<div class="mx-auto rounded-lg">
				<PrismicImage
					field={slice.primary.image}
					class="object-contain grow shrink self-stretch my-auto rounded-lg aspect-square w-[230px]  h-[230px]"
				/>
			</div>
		{/if}
	</div>
</section>
