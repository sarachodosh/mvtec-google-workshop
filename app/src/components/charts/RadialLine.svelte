<script>
    import { lineRadial } from 'd3-shape';
    import { scaleTime, scaleLinear } from 'd3-scale';

    export let data;

</script>

<div class='graphic {layout}' bind:clientWidth={width} bind:clientHeight={height}>
    <svg xmlns:svg='https://www.w3.org/2000/svg'
        viewBox='0 0 {width} {height}'
        {width}
        {height}
        >

        <g>
            <path 
                d={radialLine(data)}
                stroke={color}
                fill='none'
            />
        </g>

    </svg>
</div>