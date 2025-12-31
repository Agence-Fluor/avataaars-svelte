<!-- Selector.svelte -->
<script lang="ts">
	import { getContext, onMount, onDestroy } from 'svelte';
	import type OptionContext from './OptionContext.js';
	import type Option from './Option.js';

	let {
		option,
		defaultOption,
		components,
		restProps = {}
	}: {
		option: Option;
		defaultOption: { component: any; optionValue: string };
		components: { component: any; optionValue: string }[];
		restProps?: any;
	} = $props();

	const optionContext: OptionContext = getContext('optionContext');

	let selectedComponent: any = $state(null);

	function updateOptionValues() {
		const values = components.map((c) => c.optionValue);
		const uniqueValues = Array.from(new Set(values));

		if (uniqueValues.length !== values.length) {
			throw new Error('Duplicate values in components optionValues');
		}

		optionContext.setOptions(option.key, values);
	}

	function optionContextUpdate() {
		selectedComponent = getSelectedComponent();
	}

	function getSelectedComponent() {
		const value = optionContext.getValue(option.key);
		for (const c of components) {
			if (c.optionValue === value) {
				return c.component;
			}
		}

		return null;
	}

	onMount(() => {
		const defaultValue =
			typeof defaultOption === 'string' ? defaultOption : defaultOption.optionValue;

		// optionContext.addStateChangeListener(optionContextUpdate);
		optionContext.optionEnter(option.key);
		const optionState = optionContext.getOptionState(option.key);

		updateOptionValues();

		if (optionState) {
			optionContext.setDefaultValue(option.key, defaultValue);
		}

		selectedComponent = getSelectedComponent();
	});

	const unsubscribeState = optionContext.state.subscribe(optionContextUpdate);
	const unsubscribeData = optionContext.data.subscribe(optionContextUpdate);

	onDestroy(() => {
		// optionContext.removeStateChangeListener(optionContextUpdate);
		optionContext.optionExit(option.key);
		unsubscribeState();
		unsubscribeData();
	});
</script>

{#if selectedComponent}
	<!-- Pass down all additional props to the selected component -->
	<svelte:component this={selectedComponent} {...restProps} />
{/if}
