<script >
    import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@4/dist/runtime.js";
    import define from "https://api.observablehq.com/@sechodosh/google-trends.js?v=3";
    new Runtime().module(define, name => {
      if (name === "beeswarm") return new Inspector(document.querySelector("#observablehq-beeswarm-9630e103"));
    });
</script>
    
<div id="observablehq-beeswarm-9630e103"></div>
