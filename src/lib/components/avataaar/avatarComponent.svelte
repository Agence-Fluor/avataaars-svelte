<!-- AvatarComponent.svelte -->
<script lang="ts">
	import { onMount, setContext } from 'svelte';
	import Avatar from './avatar/avatar.svelte';
	import { allOptions, OptionContext } from './options/options.js';
	import { svgToBlob } from './utils/svg2blob.js';

	// Props
	let {
		getBlob = null as ((blob: Blob) => void) | null,
		avatarStyle = 'Circle',
		className = '',
		style = '',
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
		skinColor = '',
		backgroundColor = 'none', // Default: transparent (original: '#65C9FF')
		blobUrl = $bindable('')
	}: {
		getBlob?: ((blob: Blob) => void) | null;
		avatarStyle?: string;
		className?: string;
		style?: string;
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
		blobUrl?: string;
	} = $props();

	let avatarRef = $state<SVGSVGElement | undefined>(undefined);

	// OptionContext
	let optionContext = new OptionContext(allOptions);
	let blob: Blob | null = null;

	// Set context
	setContext('optionContext', optionContext);

	// Update optionContext when props change
	$effect(() => {
		// Access all props directly in the effect to track dependencies
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
	});

	// Function to wait for avatarRef to be available
	function waitForAvatarRef(): Promise<void> {
		return new Promise((resolve) => {
			const checkRef = setInterval(() => {
				if (avatarRef) {
					clearInterval(checkRef);
					resolve();
				}
			}, 50);
		});
	}

	onMount(async () => {
		// Wait for avatarRef to be ready and then create the blob
		await waitForAvatarRef();
		if (avatarRef) {
			blob = await svgToBlob(avatarRef);
			getBlob && getBlob(blob);
		}
	});

	$effect(() => {
		if (blob && getBlob) {
			getBlob(blob);
			blobUrl = URL.createObjectURL(blob);
		}
	});
</script>

<Avatar bind:avatarRef {avatarStyle} {style} {className} />
