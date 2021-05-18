<script>
    import * as d3 from 'd3';
import { onMount } from 'svelte';

    export let data;
    let width, height;
    export let margin = {top: 20, right: 5, bottom: 20, left: 5};

    const max_val = d3.max(data, d => d.value)

    const categories = ["mental health", "location", "climate", "social problem", "health", "natural disaster"];

    const colors = ['#ec4977', '#ff9063', '#ffd577', '#baf29d', '#00dcd5', '#0cb4f5'];
    const colorScale = d3.scaleOrdinal().domain(categories).range(colors);

    export let dots = [];
    export let forces = [];

    let renderedDots = [];

    $: xScale = d3.scaleTime()
        .domain(d3.extent(data, d => d.month))
        .range([0, chartWidth])
        .clamp(true);
    
    $: rScale = d3.scaleSqrt()
        .domain([0, max_val])
        .range([0, 12]);

    onMount(() => 
        force = d3.forceSimulation(data)
        .force('forceX', d3.forceX(d => xScale(d.month)).strength(1))
        .force('forceY', d3.forceY(chartHeight/2).strength(0.1))
        .force('collide', d3.forceCollide(d => rScale(d.value) + 0.75))
        .stop();
        
    const iterations = 100;

    for (let i = 0; i < iterations; ++i) {
        force.tick();
    };

    force.stop();


</script>

<div class='graphic' bind:clientWidth={width} bind:clientHeight={height}>
    {#if width}
    <svg xmlns:svg='https://www.w3.org/2000/svg' 
        viewBox='0 0 {width - margin.right - margin.left} {height}'
        {width}
        {height}
        role='img'
        aria-labelledby='title desc'
        >
        <g>
            {#each renderedDots as d}
                <circle 
                    stroke={colorScale(d.category)}
                    stroke-width='1'
                    cx={d.x}
                    cy={d.y}
                    r={d.r}
                    fill={colorScale(d.category)}
                />
            {/each}
        </g>
    </svg>   
    {/if} 
</div>



