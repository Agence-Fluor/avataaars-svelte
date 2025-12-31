<!-- Skin.svelte -->
<script lang="ts">
	import { SkinOption } from '../../options/options.js';
	import Selector from '../../options/Selector.svelte'; //'../../options/Selector.svelte';
	import Black from './Colors/Black.svelte';
	import Brown from './Colors/Brown.svelte';
	import DarkBrown from './Colors/DarkBrown.svelte';
	import Light from './Colors/Light.svelte';
	import Pale from './Colors/Pale.svelte';
	import Tanned from './Colors/Tanned.svelte';
	import Yellow from './Colors/Yellow.svelte';

	let { maskID }: { maskID: string } = $props();

	const components = [
		{ component: Tanned, optionValue: 'Tanned' },
		{ component: Yellow, optionValue: 'Yellow' },
		{ component: Pale, optionValue: 'Pale' },
		{ component: Light, optionValue: 'Light' },
		{ component: Brown, optionValue: 'Brown' },
		{ component: DarkBrown, optionValue: 'DarkBrown' },
		{ component: Black, optionValue: 'Black' }
	];

	const option = SkinOption;
	const defaultOption = { component: Light, optionValue: 'Light' };
</script>

<Selector {option} {defaultOption} {components} restProps={{ maskID }} />
