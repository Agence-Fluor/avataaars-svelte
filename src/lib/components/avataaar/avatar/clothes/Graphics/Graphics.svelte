<!-- Graphics.svelte -->
<script lang="ts">
	import { GraphicOption } from '../../../options/options.js';
	import Skull from './Skull.svelte';
	import Bat from './Bat.svelte';
	import Cumbia from './Cumbia.svelte';
	import Deer from './Deer.svelte';
	import Diamond from './Diamond.svelte';
	import Hola from './Hola.svelte';
	import Pizza from './Pizza.svelte';
	import Resist from './Resist.svelte';
	import Selena from './Selena.svelte';
	import Bear from './Bear.svelte';
	import SkullOutline from './SkullOutline.svelte';
	import Selector from '../../../options/Selector.svelte';

	let { maskID }: { maskID: string } = $props();

	const option = GraphicOption;
	const defaultOption = { component: Skull, optionValue: 'Skull' };

	const components = [
		{ component: Bat, optionValue: 'Bat' },
		{ component: Cumbia, optionValue: 'Cumbia' },
		{ component: Deer, optionValue: 'Deer' },
		{ component: Diamond, optionValue: 'Diamond' },
		{ component: Hola, optionValue: 'Hola' },
		{ component: Pizza, optionValue: 'Pizza' },
		{ component: Resist, optionValue: 'Resist' },
		{ component: Selena, optionValue: 'Selena' },
		{ component: Bear, optionValue: 'Bear' },
		{ component: SkullOutline, optionValue: 'SkullOutline' },
		{ component: Skull, optionValue: 'Skull' }
	];
</script>

<Selector {option} {defaultOption} {components} {maskID} />
