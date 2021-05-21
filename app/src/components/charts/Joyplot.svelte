<script>
	import Axis from '../common/Axis.svelte';
	import PointInteractive from '../common/PointInteractive.svelte';
	import Tooltip from '../common/Tooltip.svelte';
	import {line, area} from 'd3-shape';
    import {scaleTime, scaleLinear, scalePoint, scaleOrdinal} from 'd3-scale';
    import {max, extent, groups, bisector, range, bisect} from 'd3-array'
	import { timeParse, timeFormat } from 'd3-time-format';
	
    import { Delaunay } from 'd3-delaunay'
    
    export let data;
	export let margin = {top: 50, right: 5, bottom: 20, left: 100};
	export let options;
	let { key, curve, layout, format } = options;
	let datum, width, tip,tooltipOptions; //height went here
	data.forEach(date => date.date = new Date(date.month));
    data.forEach(value => value.value = +value.value);
    
	var formatMonthYear = timeFormat("%B %Y");
	
	const dataGrouped = groups(data, d => d.term);
	
	// adding index for spacing joy plot
	for (let i=0; i<dataGrouped.length; ++i) {
		dataGrouped[i].push(i);
	}
	const overlap = 0.8;
	const spacing = 20;
	var height = dataGrouped.length * spacing;
	// const colors = ['#ec4977', '#ff9063', '#ffd577', '#baf29d', '#00dcd5', '#0cb4f5'] //old
	const colors = ["#002869", "#873378", "#d55369", "#f58054", "#fba245", "#f3c73e"];
	const terms = ['mental health', 'location', 'climate', 'social problem', 'health', 'natural disaster']
	const colorScale = scaleOrdinal()
		.domain(terms)
		.range(colors)
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
		.domain([0, max(data, d => d.value)])
		.range([0, -overlap * y.step()])
	$: path = line()
		.x(d => x(d.date))
		.y(d => z(d.value))
        .curve(curve);
	$: filledPath = area()
		.x(d => x(d.date))
		.y0(0)
		.y1(d => z(d.value))
		.curve(curve)
    /* $: delaunay = Delaunay.from(dataTooltip, d => x(d.date), d => y(d.value)) */
	///////////////
	const mouseMove = (m) => {
        const mX = (m.offsetX) ? m.offsetX : m.clientX;
        const mY = (m.offsetY) ? m.offsetY : m.clientY;
        const _data = [...dataGrouped];
        const Ydomain = y.domain(); 
        const Yrange = y.range();
		console.log(Ydomain)
        const rangePoints = range(Yrange[0], Yrange[1], y.step())
        const indexTerm = Ydomain[bisect(rangePoints, mY)];
        const i = _data.findIndex(d => d[0]=== indexTerm);
        const indexDate = x.invert(mX);
        const j = bisector(d => d.date).center(_data[i][1], indexDate);
        // console.log("i:"+i);
        // console.log("index:"+indexDate);
        // console.log("j:"+j);
        // console.log("index:"+indexTerm);
        datum = _data[i][1][j]
		var tipItems = [datum.term, formatMonthYear(datum.date),[`Index: `+datum.value]].join("<br/>");
		console.log(tipItems)
        tip = (datum !== undefined)
            ? tipItems
            :``
        tooltipOptions = {x: mX,y: mY, tip: tip, visible: 1}
    }
	///////////////
	/* const mouseMove = (m) => {
		const mX = (m.offsetX) ? m.offsetX : m.clientX;
		const mY = (m.offsetY) ? m.offsetY : m.clientY;
		console.log(m.offsetX)
		const _data = [...dataGrouped];
		_data.sort((a,b) => a[key.x] - b[[key.x]]);
		const index = x.invert(mX);
		const i = bisector(d => d[key.x]).center(_data, index);
		datum = _data[i];
		tip = (datum !== undefined)
			?[datum.date,datum.value,datum.term]
			:``;
		tooltipOptions = {x: mX,y: mY, tip: tip, visible: 1}
	} */
	const leave = (m) => {
		tooltipOptions = {x: -1000, y: -1000, tip: '', visible: false}
	}
   $: hilite = (key) => {
        if(datum) return (datum.term === key) ? 1 : .5 ;
        else return 0.5;
    } 
</script> 

<div class='graphic-tall {layout}' bind:clientWidth={width} height={height}>
{#if width}
<svg xmlns:svg='https://www.w3.org/2000/svg' 
	viewBox='0 0 {width-margin.left} {height}'
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
		<text 
			transform='translate({margin.left}, {y(d[0])})'
			text-anchor='end'
			style="font-size:12px"
		>{d[0]}</text>
		<path 
			d={filledPath(d[1])}
			stroke='none'
            fill={colorScale(d[1][0]['category'])}
			opacity={hilite(d[0])}
			transform='translate(5, {y(d[0])})'
        />
		<path 
			d={path(d[1])}
			stroke={colorScale(d[1][0]['category'])}
			stroke-width='1.5'
            fill='none'
			opacity={hilite(d[0].key)}
			transform='translate(5, {y(d[0])})'
        />
        {/each}

	</g>


	<!-- <Axis {width} {height} {margin} scale={y} position='left'/> -->
	<Axis {width} {height} {margin} scale={x} position='bottom' format={format.x} />


	
	<!-- transform='translate({d[2]*100}, 0)' -->

</svg>
<Tooltip {... tooltipOptions} {width} {height} />
{/if}
</div>

<style>
    path {
        transition: opacity .3s;
    }
</style>