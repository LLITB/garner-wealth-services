<script lang="ts">
	import type { Content } from '@prismicio/client';
	import PrismicRichText from '$lib/components/PrismicRichText.svelte';
	import { PrismicLink } from '@prismicio/svelte';
	export let slice: Content.CallToActionSlice;
	// console.log('cta:', slice);
</script>

<section
	class="bg-cyan-700 py-4 md:py-6"
	data-slice-type={slice.slice_type}
	data-slice-variation={slice.variation}
>
	<!-- {slice} -->
	<div
		class="flex flex-wrap gap-6 justify-center mx-auto items-center px-52 py-4 w-full min-h-[80px] max-w-7xl md:px-5 md:max-w-full"
	>
		<div
			class="self-stretch my-auto text-xl text-center md:text-left leading-tight min-w-[240px] tracking-[2px] max-md:max-w-full text-white"
		>
			<PrismicRichText field={slice.primary.call} />
		</div>
		<div>
			<PrismicLink
				field={slice.primary.action}
				class="self-stretch px-6 py-4 my-auto text-lg leading-none bg-cyan-700 text-white border border-white border-solid max-md:px-5 rounded-lg"
			>
				{slice.primary.action.text || 'Learn More'}
			</PrismicLink>
		</div>
	</div>
</section>
