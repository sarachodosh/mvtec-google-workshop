<script>
	import { pack, hierarchy } from 'd3-hierarchy'
	import { group } from 'd3-array'
    import Tooltip from '../common/Tooltip.svelte'
import { detach_dev } from 'svelte/internal';
	
	// import { getContext } from 'svelte';
	//const { width, height, data } = getContext('LayerCake');
    export let data;
 	let width, height
	export let margin = {top: 5, right: 5, bottom: 5, left: 5};
//     // export let name = '';
//     export let idKey = 'id';
//     export let parentKey = undefined;
//     export let valueKey = 'value';
//     export let fill = '#fff';
//     export let labelVisibilityThreshold = r => r > 25;
// // 	// export let stroke = '#999';
//     export let textColor = '#333';
//     export let textStroke = 0;
//  	export let textStrokeColor = '#000';
// 	export let sortBy = (a, b) => b.value - a.value; // 'depth' is also a popular choice
   export let circlePadding = 3;
  /* --------------------------------------------
   * This component will automatically group your data
   * into one group if no `parentKey` was passed in.
   * Stash $data here so we can add our own parent
   * if there's no `parentKey`
   */
   let mapData = group(data, d => d.category);
    
	$: packer = pack()
		.size([width, height])
		.padding(circlePadding);
	$: root = hierarchy(mapData)
        .sum(d => d.value);
	$: packed = packer(root);
    $: descendants = packed.descendants();
    // const colors = ['#FA6850', '#532e75', '#873378', '#b23e74', '#d55369', '#01609A'] //old
    const colors = ["#002869", "#873378", "#d55369", "#f58054", "#fba245", "#f3c73e"];
    
    const terms = ['mental health', 'location', 'climate', 'social problem', 'health', 'natural disaster']
    $: descendants.forEach(d => {
        d.depth === 0 ? d.color = 'lightgray' :
                    d.depth === 1 ? d.color = colors[terms.indexOf(d.data[0])] :
                    d.color = colors[terms.indexOf(d.data.category)]
  });
	
// 	const titleCase = d => d.replace(/^\w/, w => w.toUpperCase());
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
    <!-- create circles -->
    {#each descendants as d}
        <circle 
            stroke={d.color}
            stroke-width = '1'
            cx={d.x}
            cy={d.y}
            r={d.r}
            fill={d.color}
            opacity={d.height === 0 ? '0.8' : '0.4'}
        />
    {/each}
    <!-- create circle labels (groups excluded) -->
    {#each descendants.filter(d=>!d.children) as d}
        {#if d.r > 30}
            <text                 
                x={d.x}
                y={d.y}
                fill="white"
                style="font-size:13px ; font-weight: 600;"
                dominant-baseline="middle" 
                text-anchor="middle"                 
                > 
                    {d.data.term}
            </text>        
        {:else if d.r > 16 || d.data.term === 'Bees'}
            <text                 
                x={d.x}
                y={d.y}
                fill="white"
                style="font-size:10px ; font-weight: 300; "
                dominant-baseline="middle" 
                text-anchor="middle"
            > 
                {d.data.term}
            </text>  
        {/if}
    {/each}
    <!-- create group labels -->
    {#each descendants.filter(d=>d.children) as d}
        
            <text
                x={d.x-15}
                y={d.y}
                dy={-d.r}         
                fill="#212121"
                style="text-transform: uppercase; font-size:14px ; font-weight: 800;"
                stroke-width="0px"
                stroke="{d.color}"
                stroke-opacity="0.5"   
                dominant-baseline="middle" 
                text-anchor="middle"    
            > 
                {d.data[0] !== undefined?d.data[0]:''}
            </text>  

    {/each}
    <g>
</svg>   

{/if}     
</div>

<style>
    svg {
        font-family:"Nunito";
    }
</style>