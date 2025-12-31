<script lang="ts">
	import ColorComponent from './ColorComponent.svelte';
	let {
		maskID,
		selectedColor = 'BrownDark'
	}: {
		maskID: string;
		selectedColor?:
			| 'Auburn'
			| 'Black'
			| 'Blonde'
			| 'BlondeGolden'
			| 'Brown'
			| 'BrownDark'
			| 'Platinum'
			| 'Red'
			| 'SilverGray';
	} = $props();

	// Define the available colors
	const colors: {
		[key in
			| 'Auburn'
			| 'Black'
			| 'Blonde'
			| 'BlondeGolden'
			| 'Brown'
			| 'BrownDark'
			| 'Platinum'
			| 'Red'
			| 'SilverGray']: string;
	} = {
		Auburn: '#A55728',
		Black: '#2C1B18',
		Blonde: '#B58143',
		BlondeGolden: '#D6B370',
		Brown: '#724133',
		BrownDark: '#4A312C',
		Platinum: '#ECDCBF',
		Red: '#C93305',
		SilverGray: '#E8E1E1'
	};

	// Get the color value based on the selected color
	let colorValue = $derived(colors[selectedColor] || colors['BrownDark']);
</script>

<ColorComponent name={selectedColor} color={colorValue} {maskID} />
