<script>
	import { getContext } from 'svelte';

	const { data, xGet, yGet, zGet, xScale, yScale, xRange, yRange, xDomain, yDomain } = getContext('LayerCake');

	$: path = values => {
        // console.log(values)
		return 'M' + values
			.map(d => {
				return $xGet(d) + ',' + $yGet(d);
			})
			.join('L');
	};
</script>

<g class="line-group">
	{#each $data as group}
		<path
			class='path-line'
			d='{path(group.values)}'
			stroke="#000"
		></path>
	{/each}
</g>

<style>
	.path-line {
		fill: none;
		stroke-linejoin: round;
		stroke-linecap: round;
		stroke-width: 1.5px;
	}
</style>