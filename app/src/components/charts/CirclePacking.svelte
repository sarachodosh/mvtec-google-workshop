<script>
	import { pack, hierarchy } from 'd3-hierarchy'
	import { group } from 'd3-array'
    import Tooltip from '../common/Tooltip.svelte'
	
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


  const colors = ['#EC4977', '#FF9063', '#FFD577', '#BAF29D', '#00DCD5', '#0CB4F5']
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

            <text                 
                x={d.x- (d.r/2)}
                y={d.y}
                style="font-size:12px ; font-weight: 300;"
                 
                > 
                    {d.data.term}
            </text>
        
    {/each}
    <g>
</svg>   

{/if}     
</div>

<style>
    
</style>
