<script>
    import { getContext } from 'svelte';
    import { forceSimulation, forceX, forceY, forceCollide } from 'd3-force';

    const { data, xGet, width, height, rGet, zGet } = getContext('LayerCake');

    const nodes = $data.map(d => ({ ...d }));
    nodes.forEach(date => date.date = new Date(date.month));
    nodes.forEach(date => date.dateNum = +date.monthNum);
    nodes.forEach(value => value.value = +value.value);
    
    console.log(nodes[0])
    console.log(typeof nodes[0]['dateNum'])
    console.log(typeof nodes[0]['value'])

    export let r = 4;
    export let xStrength = 0.95;
    export let yStrength = 0.075;
    export let strokeWidth = 1;
    export let strokeColor = '#fff';
    export let fillColor = '#000';

    $: simulation = forceSimulation(nodes)
		.force('x', forceX().x(d => $xGet(d)).strength(xStrength))
		.force('y', forceY().y($height / 2).strength(yStrength))
		.force('collide', forceCollide(r))
		.stop();

    const iterations = 10;

	$: {
		for (let i = 0; i < iterations; ++i) {
            simulation.tick();
        }
	}
</script>

<g class='bee-group'>
    {#each simulation.nodes() as node}
        <circle 
            stroke={strokeColor}
            stroke-width={strokeWidth}
            cx='{node.x}'
            cy='{node.y}'
            r={r}
            fill={fillColor || $zGet(node)}
        >

        </circle>
    {/each}
</g>