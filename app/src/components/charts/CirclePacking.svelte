<script>
<<<<<<< HEAD
	import { pack, hierarchy } from 'd3-hierarchy'
	import { group } from 'd3-array'
    import Tooltip from '../common/Tooltip.svelte'
import { detach_dev } from 'svelte/internal';
	
=======
	import { stratify, pack, hierarchy } from 'd3-hierarchy'
	import { group } from 'd3-array'
	import { scaleOrdinal } from 'd3-scale'
	import { schemeCategory10 } from 'd3-scale-chromatic'
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce
	// import { getContext } from 'svelte';

	//const { width, height, data } = getContext('LayerCake');
    export let data;

<<<<<<< HEAD
 	let width, height
	export let margin = {top: 5, right: 5, bottom: 5, left: 5};
=======
 	let width, height;
	export let margin = {top: 20, right: 5, bottom: 20, left: 5};
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce

//     // export let name = '';
//     export let idKey = 'id';
//     export let parentKey = undefined;
//     export let valueKey = 'value';
<<<<<<< HEAD
//     export let fill = '#fff';
//     export let labelVisibilityThreshold = r => r > 25;
// // 	// export let stroke = '#999';
//     export let textColor = '#333';
//     export let textStroke = 0;
//  	export let textStrokeColor = '#000';
=======
//     // export let labelVisibilityThreshold = r => r > 25;
//     // export let fill = '#fff';
// 	// export let stroke = '#999';
// 	// export let textColor = '#333';
// 	// export let textStroke = 0;
// 	// export let textStrokeColor = '#000';
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce

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

<<<<<<< HEAD
    $: descendants = packed.descendants();

    const colors = ['#EC4977', '#FF9063', '#FFD577', '#BAF29D', '#00DCD5', '#0CB4F5']
    const terms = ['mental health', 'location', 'climate', 'social problem', 'health', 'natural disaster']
    $: descendants.forEach(d => {
        d.depth === 0 ? d.color = 'lightgray' :
                    d.depth === 1 ? d.color = colors[terms.indexOf(d.data[0])] :
                    d.color = colors[terms.indexOf(d.data.category)]
  });

	
=======
  $: descendants = packed.descendants();


  const colors = ['#EC4977', '#FF9063', '#FFD577', '#BAF29D', '#00DCD5', '#0CB4F5']
  const terms = ['mental health', 'location', 'climate', 'social problem', 'health', 'natural disaster']
  $: descendants.forEach(d => {
    d.depth === 0 ? d.color = 'lightgray' :
                d.depth === 1 ? d.color = colors[terms.indexOf(d.data[0])] :
                d.color = colors[terms.indexOf(d.data.category)]
  });
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce
// 	const titleCase = d => d.replace(/^\w/, w => w.toUpperCase());
</script>

<div class='graphic' bind:clientWidth={width} bind:clientHeight={height}>
{#if width}
<<<<<<< HEAD

=======
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce
<svg xmlns:svg='https://www.w3.org/2000/svg' 
    viewBox='0 0 {width - margin.right - margin.left} {height}'
    {width}
    {height}
    role='img'
    aria-labelledby='title desc'
<<<<<<< HEAD
>
	<g>
    <!-- create circles -->
=======
    >
	<g>
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce
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
<<<<<<< HEAD
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
                fill={d.color}
                style="font-size:25px ; font-weight: 900;  text-shadow: 1px 1px 1px #fff,3px 3px 14px {d.color};"
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

=======
    <g>
</svg>   
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce
{/if}     
</div>

<style>
<<<<<<< HEAD
    svg {
        font-family:"Nunito";
    }
=======
>>>>>>> 94d518a81bc9ffb6ee588beb84b91f478db2fbce
</style>
