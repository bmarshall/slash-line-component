<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let baseSlashLine = { };
	export let comparatorSlashLine = { };

	const generateStatStyle = (baseValue, comparatorValue) =>
		comparatorValue > baseValue ? 'above-average ' : 'below-average';

	const formatPercentage = (val) => val.toFixed(3).substring(1);

	$:({name, avg, obp, slg} = comparatorSlashLine);
	$:({avg: baseAvg, obp: baseObp, slg: baseSlg} = baseSlashLine);
	$:toClickHandler = (prop) => () => dispatch('statClicked', {name, stat:prop, difference: comparatorSlashLine[prop] - baseSlashLine[prop] })

</script>

{#if name}
	<div>
		{name}
		<span class={generateStatStyle(baseAvg, avg)} on:click={toClickHandler('avg')} >{formatPercentage(avg)}</span> /
		<span class={generateStatStyle(baseObp, obp)} on:click={toClickHandler('obp')}>{formatPercentage(obp)}</span> /
		<span class={generateStatStyle(baseSlg, slg)} on:click={toClickHandler('slg')}>{formatPercentage(slg)}</span>
	</div>
{:else}
	- -/-/-
{/if}

<style>
	.above-average {
		background-color: #DC143C;
		color: #ffffff;
	}

	.below-average {
		background-color: #0000FF;
		color: #ffffff;
	}
</style>