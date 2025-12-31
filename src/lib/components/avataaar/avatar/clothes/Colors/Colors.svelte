<!-- Colors.svelte -->
<script lang="ts">
	import Black from './Black.svelte';
	import Blue01 from './Blue01.svelte';
	import Blue02 from './Blue02.svelte';
	import Blue03 from './Blue03.svelte';
	import Gray01 from './Gray01.svelte';
	import Gray02 from './Gray02.svelte';
	import Heather from './Heather.svelte';
	import PastelBlue from './PastelBlue.svelte';
	import PastelGreen from './PastelGreen.svelte';
	import PastelOrange from './PastelOrange.svelte';
	import PastelRed from './PastelRed.svelte';
	import PastelYellow from './PastelYellow.svelte';
	import Pink from './Pink.svelte';
	import Red from './Red.svelte';
	import White from './White.svelte';
	import { ClotheColorOption } from '../../../options/options.js';
	import Selector from '../../../options/Selector.svelte';

	let { maskID }: { maskID: string } = $props();

	const components = [
		{ component: Black, optionValue: 'Black' },
		{ component: Blue01, optionValue: 'Blue01' },
		{ component: Blue02, optionValue: 'Blue02' },
		{ component: Blue03, optionValue: 'Blue03' },
		{ component: Gray01, optionValue: 'Gray01' },
		{ component: Gray02, optionValue: 'Gray02' },
		{ component: Heather, optionValue: 'Heather' },
		{ component: PastelBlue, optionValue: 'PastelBlue' },
		{ component: PastelGreen, optionValue: 'PastelGreen' },
		{ component: PastelOrange, optionValue: 'PastelOrange' },
		{ component: PastelRed, optionValue: 'PastelRed' },
		{ component: PastelYellow, optionValue: 'PastelYellow' },
		{ component: Pink, optionValue: 'Pink' },
		{ component: Red, optionValue: 'Red' },
		{ component: White, optionValue: 'White' }
	];

	const option = ClotheColorOption;
	const defaultOption = { component: Gray01, optionValue: 'Gray01' };
</script>

<Selector {option} {defaultOption} {components} restProps={{ maskID }} />
