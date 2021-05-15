<script>
	//Import components
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleOrdinal } from 'd3-scale';
	import Beeswarm from '../components/charts/Beeswarm.svelte'; 
    import Joyplot from '../components/charts/Joyplot.svelte';

    import { timeParse, timeFormat } from 'd3-time-format';
    import { format, precisionFixed } from 'd3-format';

    // import Multiline from '../components/charts/Multiline_example.svelte'
    import Axis from '../components/common/Axis.svelte';
    // import Labels from '../components/common/Labels.svelte';
    import SharedTooltip from '../components/common/Tooltip.svelte';

    // import weather2 from '../data/weather2.json';
    // import {curveMonotoneX} from 'd3-shape'


	import dataB from '../data/dataB_long.csv';
    import dataA from '../data/dataA_long.csv';
    import { curveCatmullRom } from 'd3-shape';
    
    // For beeswarm
	const xKey = 'dateNum'; // NEED TO CHANGE THIS TO dateNum!
    const zKey = 'category';
    const rKey = 'value';
	const r = 4;

    const colors = ['#ec4977', '#ff9063', '#ffd577', '#baf29d', '#00dcd5', '#0cb4f5'];

</script>



<Joyplot
    data={dataB}
    options={
        {
			curve: curveCatmullRom,
            layout: 'col'
        }
    }
/>




<!-- <div class='chart-container'>
    <LayerCake 
        padding={{bottom: 15}}
        x={xKey}
        data={dataA}
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
</div> -->


