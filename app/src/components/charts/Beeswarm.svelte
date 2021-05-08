<script>
    import { getContext } from 'svelte';
    import { forceSimulation, forceX, forceY, forceCollide } from 'd3-force';

    const { data, xGet, height, zGet, custom } = getContext('LayerCake');

    const nodes = $data.map((d) => ({ ...d }));
    // console.log(nodes)

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

	$: {
		for ( var i = 0,
			n = 150;
			// The REPL thinks there is an infinite loop with this next line but it's generally a better way to go
			//n = Math.ceil(Math.log(simulation.alphaMin()) / Math.log(1 - simulation.alphaDecay()));
			i < n;
			++i ) {
			simulation.tick();
		}
	}
</script>

<g class='bee-group'>
    {#each simulation.nodes() as node}
        <circle 
            fill='{fillColor}'
            stroke='{strokeColor}'
            stroke-width='{strokeWidth}'
            cx='{nodes.x}'
            cy='{nodes.y}'
            r='{r}'
        >

        </circle>
    {/each}
</g>