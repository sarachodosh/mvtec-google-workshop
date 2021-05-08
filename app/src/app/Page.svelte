<script>
	//Import components
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleOrdinal } from 'd3-scale';
	// import Beeswarm from '../components/charts/Beeswarm.svelte'; 

    import { timeParse, timeFormat } from 'd3-time-format';
    import { format, precisionFixed } from 'd3-format';

    import Multiline from './components/charts/Multiline.svelte';
    import AxisX from './components/AxisX.svelte';
    import AxisY from './components/AxisY.svelte';
    import Labels from './components/Labels.svelte';
    import SharedTooltip from './components/SharedTooltip.svelte';

    //For multiline
    const xKey_multi = 'month';
    const yKey_multi = 'value';
    import multilineData from '../data/help_trends_indexB.csv';

    const seriesNames = Object.keys(data[0].filter(d => d !== xKey));
    console.log(multilineData)

    //For beeswarm
	// import beeswarmData from '../data/indexB_long.csv';
	// const xKey = 'month';
	// const r = 6;

</script>

<div class='multiline-container'>
    <Multiline/>
</div>

<!-- <div class='beeswarm-container'>
    <LayerCake 
        padding={{bottom: 15}}
        x={xKey}
        data={beeswarmData}
        let:width
    >

    <Svg>
        <Beeswarm 
            r={r}
            strokeWidth={1}
            xStrength={0.95}
            yStrength={0.075}
        />
    </Svg>

    <Html pointerEvents={false}>
    </Html>
    </LayerCake>
</div> -->

