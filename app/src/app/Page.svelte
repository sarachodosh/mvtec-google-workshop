<script>
	//Import components
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleOrdinal } from 'd3-scale';
	import Beeswarm from '../components/charts/Beeswarm.svelte'; 
    // import RadialLine from '../components/charts/RadialLine.svelte';

    import { timeParse, timeFormat } from 'd3-time-format';
    import { format, precisionFixed } from 'd3-format';

    // import Multiline from '../components/charts/Multiline.svelte';
    // import AxisX from './components/common/AxisX.svelte';
    // import AxisY from './components/common/AxisY.svelte';
    // import Labels from '../components/common/Labels.svelte';
    import SharedTooltip from '../components/common/Tooltip.svelte';


    //For beeswarm
	import dataB from '../data/dataB_long.csv';
    
	const xKey = 'dateNum'; // NEED TO CHANGE THIS TO dateNum!
    const zKey = 'category';
    const rKey = 'value';
	const r = 4;

    const colors = ['#ec4977', '#ff9063', '#ffd577', '#baf29d', '#00dcd5', '#0cb4f5'];

</script>

<style>
    .chart-container {
		width: 100%;
		height: 1000px;
	}
</style>




<div class='chart-container'>
    <LayerCake 
        padding={{bottom: 15}}
        x={xKey}
        data={dataB}
        z={zKey}
        zScale={scaleOrdinal()}
    >

    <Svg>
        <Beeswarm 
            r={r}
            strokeWidth={1}
            xStrength={0.95}
            yStrength={0.075}
        />
    </Svg>

    </LayerCake>
</div>


