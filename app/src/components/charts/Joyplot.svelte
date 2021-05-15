<script>
	import Axis from '../common/Axis.svelte';
	import PointInteractive from '../common/PointInteractive.svelte';
	import {line} from 'd3-shape';
    import {scaleTime, scaleLinear, scalePoint} from 'd3-scale';
    import {max, extent} from 'd3-array'
    import { Delaunay } from 'd3-delaunay'
	import * as d3 from 'd3'
    
    export let data;
	export let margin = {top: 500, right: 5, bottom: 20, left: 5};
	export let options;
	let { curve, layout } = options;

	let datum, width; //height went here


	data.forEach(date => date.date = new Date(date.month));
    data.forEach(value => value.value = +value.value);
    
	// console.log(data)

	const dataGrouped = d3.groups(data, d => d.term);

	// adding index for spacing joy plot
	for (let i=0; i<dataGrouped.length; ++i) {
		dataGrouped[i].push(i);
	}

	const overlap = 8;
	const spacing = 25;

	var height = dataGrouped.length * spacing;

	$: x = scaleTime()
		.domain(extent(data, d => d.date))
		.range([margin.left, width - margin.right]);
	
	// $: y = scaleLinear()
	// 	.domain([0, max(data, d => d.value)])
	// 	.range([height - margin.bottom - margin.top, margin.top]);
	
	$: y = scalePoint()
		.domain(dataGrouped.map(d => d[0]))
		.range([margin.top, height - margin.bottom - margin.top]);

	$: z = scaleLinear()
		.domain([0, d3.max(data, d => d.value)])
		.range([0, -overlap * y.step()])

	$: path = line()
		.x(d => x(d.date))
		.y(d => z(d.value))
        .curve(curve);



    $: delaunay = Delaunay.from(data, d => x(d.date), d => y(d.value))

	const mouseMove = (m) => {
        const mX = (m.offsetX) ? m.offsetX : m.clientX;
        const mY = (m.offsetY) ? m.offsetY : m.clientY;
        const picked = delaunay.find(mX, mY);
        datum = dataGrouped[picked];
	}

	const leave = (m) => {
		datum = null;
    }
    
    $: hilite = (key) => {
        if(datum) return (datum.key === key) ? 1 : .3 ;
        else return 1;
    }

	

</script> 

<div class='graphic-tall {layout}' bind:clientWidth={width} height={height}>
{#if width}
<svg xmlns:svg='https://www.w3.org/2000/svg' 
	viewBox='0 0 {width} {height}'
	{width}
	{height}
	role='img'
    aria-labelledby='p'
    on:touchmove|preventDefault
	on:pointermove|preventDefault={mouseMove}
	on:mouseleave={leave}
	on:touchend={leave}
	>
	<!-- <title id='title'>{title}</title> -->
	<!-- <desc id='desc'>{desc}</desc> -->
	<g>
        {#each dataGrouped as d}
		<p>TK</p>
		<path 
			d={path(d[1])}
			stroke='#000'
            fill='none'
            opacity='1'
			transform='translate(0, {d[2]*spacing})'
        />
        {/each}
	</g>

	<!-- <Axis {width} {height} {margin} scale={y} position='left' format={format.y} /> -->
	<!-- <Axis {width} {height} {margin} scale={x} position='bottom' format={format.x} /> -->

	<!-- <PointInteractive {datum} {format} {x} {y} key={{x:'x', y:'y'}} {width} /> -->
	
	<!-- transform='translate({d[2]*100}, 0)' -->

</svg>
{/if}
</div>

<style>
    path {
        transition: opacity .3s;
    }
</style>