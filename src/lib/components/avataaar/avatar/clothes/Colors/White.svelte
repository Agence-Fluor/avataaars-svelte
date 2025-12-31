<!-- White.svelte -->
<script lang="ts">
	let { maskID }: { maskID: string } = $props();
	export const optionValue = 'White';
</script>

<g id="Color/Palette/White" mask={'url(#' + maskID + ')'} fill-rule="evenodd" fill="#FFFFFF">
	<rect id="🖍Color" x="0" y="0" width="264" height="110" />
</g>
