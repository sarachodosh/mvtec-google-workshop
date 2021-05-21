<script>
  import { getContext } from 'svelte';
  import { forceSimulation, forceX, forceY, forceCollide } from 'd3-force';
  import { extent, max } from 'd3-array';
  import { scaleLinear, scaleOrdinal, scaleSqrt } from 'd3-scale'
  //const { data, xGet, width, height, rGet, zGet } = getContext('LayerCake');
  export let data;
  export let xKey;
  export let rKey;
  export let zKey;
  export let colors;
  export let rThreshold = 0.5; //Value below that the circle is removed (for performance issues)
  let width, height;
  export let margin = {top: 20, right: 20, bottom: 20, left: 20};
  const nodes = data.filter(d=>d[rKey]>rThreshold).map(d => ({ ...d }));
  nodes.forEach(date => date.date = new Date(date.month));
  nodes.forEach(date => date.dateNum = +date.monthNum);
  nodes.forEach(value => value.value = +value.value);
  
  // console.log(nodes.length);
  // console.log(NaNchecker(nodes.dateNum))
  // function NaNchecker(array) {
  //     for (let i=0; i < array.length; ++i){
  //     // check if array value is false or NaN
  //         if (isNaN(array[i])) {
  //             console.log("Not a number at index " + i + ": "+array[i]);
  //         }
  //     }
  // }
  export let r = 14;
  export let xStrength = 0.5;
  export let yStrength = 0.09;
  export let strokeWidth = 0;
  export let strokeColor = '#c5cae9';
  export let fillColor = '#cecece';

  $: xScale = scaleLinear()
          .domain(extent(nodes, d=>d[xKey]))
          .range([margin.left, width-margin.right]);

  $: unique_cats = [...new Set(data.map(d => d[zKey]))];

  $: colorScale = scaleOrdinal()
          .domain(unique_cats)
          .range(colors);

  $: rScale = scaleSqrt()
          .domain([0, max(nodes, d=>d[rKey])])
          .range([0, r]);

  $: simulation = forceSimulation(nodes)
      .force('x', forceX().x(d => xScale(d[xKey])).strength(xStrength))
      .force('y', forceY().y(height / 2).strength(yStrength))
      .force('collide', forceCollide(d => rScale(d[rKey]*1.3)))
      .stop();

  const iterations = 200;

  $: {
    for (let i = 0; i < iterations; ++i) {
            simulation.tick();
        }
  }

 

</script>

<div class='graphic' bind:clientWidth={width} bind:clientHeight={height}>
  {#if width}
  <svg xmlns:svg='https://www.w3.org/2000/svg' 
      viewBox='0 0 {width} {height}'
      {width}
      {height}
      role='img'
      aria-labelledby='title desc'
      >
      <g class='bee-group'>
          {#each simulation.nodes() as node}
              <circle 
                  stroke={strokeColor}
                  stroke-width={strokeWidth}
                  cx={node.x}
                  cy={node.y}
                  r={rScale(node[rKey])}
                  fill={colorScale(node[zKey]) || fillColor}
              >
              <!-- colorScale(node[zKey]) || fillColor -->
              <!-- selectCats(node[zKey]) ? colorScale(node[zKey]) : fillColor -->
              </circle>
          {/each}
      </g>
  </svg>   
  {/if}     
</div>