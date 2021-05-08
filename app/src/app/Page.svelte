<script>
	//Import components
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleOrdinal } from 'd3-scale';
	// import Beeswarm from '../components/charts/Beeswarm.svelte'; 

    import { timeParse, timeFormat } from 'd3-time-format';
    import { format, precisionFixed } from 'd3-format';

    import Multiline from '../components/charts/Multiline.svelte';
    // import AxisX from './components/AxisX.svelte';
    // import AxisY from './components/AxisY.svelte';
    // import Labels from './components/Labels.svelte';
    // import SharedTooltip from './components/SharedTooltip.svelte';

    //For multiline
    const xKey_multi = 'month';
    const yKey_multi = 'value';
    import multilineData from '../data/indexB_long.csv';
    const parseDate = timeParse('%d/%m/%y')
    multilineData.forEach(date => date.month = parseDate(date.month))
    multilineData.forEach(value => value.value = +value.value)
    const terms = ['Addiction', 'ADHD', 'Alcoholism', 'Aleppo', 'Amazon rainforest', 'Anger management', 'Anorexia', 'Anxiety', 'Australia fires', 'Bahamas', 'Bees', 'Beirut', 'Bipolar', 'Black Lives Matter', 'BPD', 'Breakup', 'Bulimia', 'Cancer', 'Climate change', 'Coronavirus', 'Depression', 'Eating disorder', 'Flint Michigan', 'Flood', 'Fort McMurray', 'Grief', 'Haiti', 'Hoarding', 'Homelessness', 'Houston', 'Hurricane Harvey', 'India', 'Kerala', 'Las Vegas', 'Louisiana', 'Mental illness', 'Migrant children', 'Narcissism', 'Nepal', 'OCD', 'Orlando', 'Palestine', 'Panic attack', 'Paris', 'Poverty', 'PTSD', 'Puerto Rico', 'Quitting smoking', 'Rape', 'Refugee', 'Schizophrenia', 'Seizure', 'Self harm', 'Self-esteem', 'Shortness of breath, covid', 'Standing Rock', 'Sudan', 'Suicidal ideation', 'Syria', 'Texas', 'Wildfire', 'Yemen']

    // console.log(multilineData)

    const dataLong = terms.map(key => {
        var valuesToAdd = [];

        multilineData.map(d => {
				if (d.term == key) {
                    valuesToAdd.push(d)
                }
			})

		return {
			key,
			values: valuesToAdd
		};
	});

    console.log(dataLong)

    //For beeswarm
	// import beeswarmData from '../data/indexB_long.csv';
	// const xKey = 'month';
	// const r = 6;

</script>

<style>
    .chart-container.svelte-pudx9b,.layercake-container.svelte-vhzpsp {
		width: 100%;
		height: 100%;
	}
</style>

<div class='chart-container'>
    <LayerCake 
        padding={{ top: 7, right: 10, bottom: 20, left: 25 }}
        x={xKey_multi}
        y={yKey_multi}
        yDomain={[0, null]}
        flatData={multilineData}
        data={dataLong}
    >
    
        <Svg>
            <Multiline/>
        </Svg>

    </LayerCake>
   
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


