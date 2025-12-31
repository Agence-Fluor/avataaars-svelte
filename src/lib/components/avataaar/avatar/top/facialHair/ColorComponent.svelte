<script lang="ts">
	let {
		name,
		color,
		maskID
	}: {
		name: string;
		color: string;
		maskID: string;
	} = $props();
</script>

<g id="Color/Hair/{name}" mask="url(#{maskID})" fill={color}>
	<g transform="translate(-32.000000, 0.000000)" id="Color">
		<rect x="0" y="0" width="264" height="244" />
	</g>
</g>
