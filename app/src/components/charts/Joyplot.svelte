<script>
	import Axis from '../common/Axis.svelte';
	import PointInteractive from '../common/PointInteractive.svelte';
	import {line} from 'd3-shape';
    import {scaleTime, scaleLinear} from 'd3-scale';
    import {max, extent} from 'd3-array'
    import { Delaunay } from 'd3-delaunay'
	import * as d3 from 'd3'
    
    export let data;
	export let margin = {top: 20, right: 5, bottom: 20, left: 5};
	export let options;
	let { curve } = options;

	let datum, width, height;

	data.forEach(date => date.date = new Date(date.month));
    data.forEach(value => value.value = +value.value);
    
	// console.log(data)

	const dataGrouped = d3.groups(data, d => d.term);

	console.log(dataGrouped)
	console.log(extent(data, d => d.date))

	$: x = scaleTime()
		.domain(extent(data, d => d.date))
		.range([margin.left, width - margin.right]);
	
	$: y = scaleLinear()
		.domain([0, max(data, d => d.value)])
		.range([height - margin.bottom - margin.top, margin.top]);

	$: path = line()
		.x(d => x(d.date))
		.y(d => y(d.value))
        .curve(curve);


    // $: delaunay = Delaunay.from(_data, d => x(d.x), d => y(d.y))

	const mouseMove = (m) => {
        const mX = (m.offsetX) ? m.offsetX : m.clientX;
        const mY = (m.offsetY) ? m.offsetY : m.clientY;
        const picked = delaunay.find(mX, mY);
        datum = _data[picked];
	}

	const leave = (m) => {
		datum = null;
    }
    
    $: hilite = (key) => {
        if(datum) return (datum.key === key) ? 1 : .3 ;
        else return 1;
    }

</script> 

<div bind:clientWidth={width} bind:clientHeight={height}>
{#if width}
<svg xmlns:svg='https://www.w3.org/2000/svg' 
	viewBox='0 0 800 800'
	{width}
	{height}
	role='img'
    aria-labelledby='title desc'
    on:touchmove|preventDefault
	on:pointermove|preventDefault={mouseMove}
	on:mouseleave={leave}
	on:touchend={leave}
	>
	<!-- <title id='title'>{title}</title> -->
	<!-- <desc id='desc'>{desc}</desc> -->
	<g>
        {#each dataGrouped as d}
		<path 
			d={path(d[1])}
			stroke='#000'
            fill='none'
            opacity='1'
        />
        {/each}
	</g>

	<!-- <Axis {width} {height} {margin} scale={y} position='left' format={format.y} /> -->
	<!-- <Axis {width} {height} {margin} scale={x} position='bottom' format={format.x} /> -->

	<!-- <PointInteractive {datum} {format} {x} {y} key={{x:'x', y:'y'}} {width} /> -->
	
</svg>
{/if}
</div>

<style>
    path {
        transition: opacity .3s;
    }
</style>