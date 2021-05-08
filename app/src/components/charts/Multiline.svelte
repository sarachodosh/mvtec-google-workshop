<script>
<<<<<<< HEAD
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
		stroke-width: 1px;
	}
=======
	import Axis from '../common/Axis.svelte';
	import PointInteractive from '../common/PointInteractive.svelte';
	import {line} from 'd3-shape';
    import {scaleTime, scaleLinear} from 'd3-scale';
    import {max, extent} from 'd3-array'
    import { Delaunay } from 'd3-delaunay'
    
    export let data;
	export let margin = {top: 20, right: 5, bottom: 20, left: 5};
	export let options;
	let {key, format, color, layout, title, desc, curve } = options;

	let datum, width, height;
    
    const _data = key.y.map( (key, i) => data.map(d => ({x: d.time, y: d[key], key:key, color: color[i]} )))
		
	$: x = scaleTime()
		.domain(extent(_data.flat(), d => d.x))
		.range([margin.left, width - margin.right]);
	
	$: y = scaleLinear()
		.domain([0, max(_data.flat(), d => d.y)])
		.range([height - margin.bottom - margin.top, margin.top]);

	$: path = line()
		.x(d => x(d.x))
		.y(d => y(d.y))
        .curve(curve);

    $: delaunay = Delaunay.from(_data.flat(), d => x(d.x), d => y(d.y))

	const mouseMove = (m) => {
        const mX = (m.offsetX) ? m.offsetX : m.clientX;
        const mY = (m.offsetY) ? m.offsetY : m.clientY;
        const picked = delaunay.find(mX, mY);
        datum = _data.flat()[picked];
	}

	const leave = (m) => {
		datum = null;
    }
    
    $: hilite = (key) => {
        if(datum) return (datum.key === key) ? 1 : .3 ;
        else return 1;
    }

</script> 

<div class='graphic {layout}' bind:clientWidth={width} bind:clientHeight={height}>
{#if width}
<svg xmlns:svg='https://www.w3.org/2000/svg' 
	viewBox='0 0 {width} {height}'
	{width}
	{height}
	role='img'
    aria-labelledby='title desc'
    on:touchmove|preventDefault
	on:pointermove|preventDefault={mouseMove}
	on:mouseleave={leave}
	on:touchend={leave}
	>
	<title id='title'>{title}</title>
	<desc id='desc'>{desc}</desc>
	<g>
        {#each _data as d}
		<path 
			d={path(d)}
			stroke={d[0].color}
            fill='none'
            opacity={hilite(d[0].key)}
        />
        {/each}
	</g>

	<Axis {width} {height} {margin} scale={y} position='left' format={format.y} />
	<Axis {width} {height} {margin} scale={x} position='bottom' format={format.x} />

	<PointInteractive {datum} {format} {x} {y} key={{x:'x', y:'y'}} {width} />
	
</svg>
{/if}
</div>

<style>
    path {
        transition: opacity .3s;
    }
>>>>>>> parent of 8dfda1a (started new svelte page)
</style>