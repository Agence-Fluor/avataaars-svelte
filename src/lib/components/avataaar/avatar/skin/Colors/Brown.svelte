<!-- Brown.svelte -->
<script lang="ts">
	let {
		maskID,
		optionValue = 'Brown'
	}: {
		maskID: string;
		optionValue?: string
	} = $props();
</script>

<g id={'Skin/' + optionValue} mask={'url(#' + maskID + ')'} fill="#D08B5B">
	<g transform="translate(0.000000, 0.000000)" id="Color">
		<rect x="0" y="0" width="264" height="280" />
	</g>
</g>
