<!-- Piece.svelte -->
<script lang="ts">
	import { onMount, setContext, $effect } from 'svelte';
	import { allOptions, OptionContext } from './options/options.js';

	// Props
	let {
		avatarStyle = '',
		style = {},
		pieceType = '',
		pieceSize = '',
		viewBox = '',
		topType = '',
		accessoriesType = '',
		hairColor = '',
		facialHairType = '',
		facialHairColor = '',
		clotheType = '',
		clotheColor = '',
		graphicType = '',
		eyeType = '',
		eyebrowType = '',
		mouthType = '',
		skinColor = ''
	}: {
		avatarStyle?: string;
		style?: any;
		pieceType?: string;
		pieceSize?: string;
		viewBox?: string;
		topType?: string;
		accessoriesType?: string;
		hairColor?: string;
		facialHairType?: string;
		facialHairColor?: string;
		clotheType?: string;
		clotheColor?: string;
		graphicType?: string;
		eyeType?: string;
		eyebrowType?: string;
		mouthType?: string;
		skinColor?: string;
	} = $props();

	// OptionContext
	let optionContext = new OptionContext(allOptions);

	// Set context
	setContext('optionContext', optionContext);

	// Collect props into an object
	let props = $derived({
		topType,
		accessoriesType,
		hairColor,
		facialHairType,
		facialHairColor,
		clotheType,
		clotheColor,
		graphicType,
		eyeType,
		eyebrowType,
		mouthType,
		skinColor
	});

	// Update optionContext when props change
	$effect(() => {
		updateOptionContext();
	});

	function updateOptionContext() {
		const data: { [key: string]: any } = {};
		for (const option of allOptions) {
			let value = null;

			if (option.key === 'topType') {
				value = topType;
			} else if (option.key === 'accessoriesType') {
				value = accessoriesType;
			} else if (option.key === 'hairColor') {
				value = hairColor;
			} else if (option.key === 'facialHairType') {
				value = facialHairType;
			} else if (option.key === 'facialHairColor') {
				value = facialHairColor;
			} else if (option.key === 'clotheType') {
				value = clotheType;
			} else if (option.key === 'clotheColor') {
				value = clotheColor;
			} else if (option.key === 'graphicType') {
				value = graphicType;
			} else if (option.key === 'eyeType') {
				value = eyeType;
			} else if (option.key === 'eyebrowType') {
				value = eyebrowType;
			} else if (option.key === 'mouthType') {
				value = mouthType;
			} else if (option.key === 'skinColor') {
				value = skinColor;
			}

			if (value) {
				data[option.key] = value;
			}
		}
		optionContext.setData(data);
	}

	onMount(() => {
		updateOptionContext();
	});
</script>

<!-- <PieceComponent {avatarStyle} {style} {pieceType} {pieceSize} {viewBox} /> -->
