<!-- Heading.svelte -->
<script lang="ts">
	type HeadingLevel = 'h1' | 'h2' | 'h3' | 'h4' | 'h5' | 'h6';
	type HeadingSize = '4xl' | '3xl' | '2xl' | 'xl';
	type IdFunction = () => string;

	// Props with default values and proper types
	export let as: HeadingLevel = 'h3';
	export let size: HeadingSize = '4xl';
	export let className: string = '';
	export let id: string | IdFunction | undefined = undefined;
	// export let id: string | undefined = undefined;
	function getIdValue(id: string | IdFunction | undefined): string | undefined {
		if (typeof id === 'function') {
			return id();
		}
		return id;
	}
	// Helper function to replace clsx functionality
	function getClasses(size: HeadingSize, additionalClasses: string): string {
		const baseClasses = 'font-sans font-semibold tracking-tighter text-cyan-700 ';
		const sizeClasses: Record<HeadingSize, string> = {
			'4xl': 'text-3xl md:text-4xl',
			'3xl': 'text-3xl',
			'2xl': 'text-2xl',
			xl: 'text-xl'
		};

		return `${baseClasses} ${sizeClasses[size]} ${additionalClasses}`.trim();
	}
</script>

<svelte:element this={as} id={getIdValue(id)} class={getClasses(size, className)}>
	<slot />
</svelte:element>
