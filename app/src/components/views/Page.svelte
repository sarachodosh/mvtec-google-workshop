<script>
  import { Parallax, ParallaxLayer } from "svelte-parallax";

  import ScatterCanvas from "../charts/ScatterCanvas.svelte";

  import { Button, ButtonGroup, ButtonGroupItem } from "svelte-materialify";

  let parallax;
  let disabled = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  const url = (name, wrap = false) =>
    `${
      wrap ? "url(" : ""
    }https://awv3node-homepage.surge.sh/build/assets/${name}.svg${
      wrap ? ")" : ""
    }`;

  let scatterStep, otherStep;

  const otherPoints = [...new Array(800)].map((d) => ({
    coords: [
      { x: Math.random() * 400, y: Math.random() * 400, r: Math.random() * 16 },
      { x: Math.random() * 400, y: Math.random() * 400, r: Math.random() * 16 },
    ],
  }));
</script>

<!-- HERO -->
<div class="hero">
  <p class="headline1">What looking for help mean?</p>
  <p class="author">
    By <span style="font-weight:600">Sara Chodosh, Xavier Bolló</span> and
    <span style="font-weight:600">Santiago Salcido</span>
  </p>
  <p class="date">May 19, 2021</p>
  <img src="searchImg.png" alt="search" width="100" height="100">
</div>

<p align="center">
  <iframe
    width="70%"
    height="382"
    frameborder="0"
    src="https://observablehq.com/embed/@sechodosh/google-trends?cells=beeswarm"
    style="align=center"
  />
</p>
<!-- <button class="disable" on:click={() => disabled = !disabled}>disable</button> -->
<!-- <div class='col'>
    <p>This is an example of how you can do smooth transitions. It uses canvas so you can do a few thousand elements. Instead of the buttons triggering which step is in view, you can use the scroll ...  </p>
    <Button on:click={() => otherStep = 0} outlined>
        Arrange like so
    </Button>
    <Button on:click={() => otherStep = 1} outlined>
        Rearrange again
    </Button>
</div>
<ScatterCanvas
    data={otherPoints}
    layout='wide'
    step={otherStep}
    mark='circle'
/> -->
<Parallax
  sections="3"
  style="background-color: #253237;"
  {disabled}
  bind:this={parallax}
>
  <ParallaxLayer offset="1" rate="1" style="background-color: #805E73;" />
  <ParallaxLayer offset="2" rate="1" style="background-color: #87BCDE;" />

  <ParallaxLayer
    offset="0"
    rate="0"
    span="3"
    style="background-image: {url('stars', true)}; background-size: cover;"
  />

  <ParallaxLayer offset="1.3" rate="-0.3">
    <img
      src={"https://42f2671d685f51e10fc6-b9fcecea3e50b3b59bdc28dead054ebc.ssl.cf5.rackcdn.com/illustrations/gradma_wanr.svg"}
      alt=""
      style="width: 15%; margin-left: 70%;"
    />
  </ParallaxLayer>

  <ParallaxLayer offset="1" rate="0.8" style="opacity: 0.1;">
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 20%; margin-left: 55%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 10%; margin-left: 15%;"
    />
  </ParallaxLayer>

  <ParallaxLayer offset="1.75" rate="0.5" style="opacity: 0.1;">
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 20%; margin-left: 70%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 20%; margin-left: 40%;"
    />
  </ParallaxLayer>

  <ParallaxLayer offset="1" rate="0.2" style="opacity: 0.2;">
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 10%; margin-left: 10%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 20%; margin-left: 75%;"
    />
  </ParallaxLayer>

  <ParallaxLayer offset="1.6" rate="-0.1" style="opacity: 0.4;">
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 20%; margin-left: 60%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 25%; margin-left: 30%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 10%; margin-left: 80%;"
    />
  </ParallaxLayer>

  <ParallaxLayer offset="2.6" rate="0.4" style="opacity: 0.6;">
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 20%; margin-left: 5%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 15%; margin-left: 75%;"
    />
  </ParallaxLayer>

  <ParallaxLayer
    offset="2.5"
    rate="-0.4"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img src={url("earth")} alt="" style="width: 60%;" />
  </ParallaxLayer>

  <ParallaxLayer
    offset="2"
    rate="-0.3"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img
      src={"https://42f2671d685f51e10fc6-b9fcecea3e50b3b59bdc28dead054ebc.ssl.cf5.rackcdn.com/illustrations/empty_street_sfxm.svg"}
      alt=""
      style="width: 50%;"
    />
  </ParallaxLayer>

  <ParallaxLayer
    offset="0"
    rate="0.1"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img
      src={"https://42f2671d685f51e10fc6-b9fcecea3e50b3b59bdc28dead054ebc.ssl.cf5.rackcdn.com/illustrations/creative_thinking_b3bc.svg"}
      alt=""
      class="server"
      style="width: 20%;"
      on:click={() => parallax.scrollTo(2, { selector: ".bash" })}
      on:keyup={(e) =>
        e.key === "Enter" && parallax.scrollTo(2, { selector: ".bash" })}
      tabindex="0"
    />
  </ParallaxLayer>

  <ParallaxLayer
    offset="1"
    rate="0.1"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img
      src={"https://42f2671d685f51e10fc6-b9fcecea3e50b3b59bdc28dead054ebc.ssl.cf5.rackcdn.com/illustrations/fall_thyk.svg"}
      alt=""
      class="bash"
      style="width: 40%;"
      on:click={() => parallax.scrollTo(3, { selector: ".clients-main" })}
      on:keyup={(e) =>
        e.key === "Enter" &&
        parallax.scrollTo(3, { selector: ".clients-main" })}
      tabindex="0"
    />
  </ParallaxLayer>

  <ParallaxLayer
    offset="2"
    rate="-0"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <iframe
      width="100%"
      height="50%"
      frameborder="0"
      src="https://observablehq.com/embed/@sechodosh/google-trends?cells=radial"
      alt=""
      class="clients-main"
      style="width: 30%;height:40%;background:white"
      on:click={() => parallax.scrollTo(1, { selector: ".server" })}
      on:keyup={(e) =>
        e.key === "Enter" && parallax.scrollTo(1, { selector: ".server" })}
      tabindex="0"
    />
  </ParallaxLayer>
</Parallax>

<style>
  :global(body) {
    padding: 0;
  }
  .server,
  .bash,
  .clients-main {
    cursor: pointer;
  }
  img:focus {
    outline: 1px dotted gray;
  }
  img:focus:not(:focus-visible) {
    outline: none;
  }
  .server:focus-visible {
    outline: 2px dotted gray;
  }
  .bash:focus-visible {
    outline: 2px dotted purple;
  }
  .clients-main:focus-visible {
    outline: 2px dotted blue;
  }
  .hero {
    max-width: 680px;
    padding-top: 144px;
    margin: auto;
    position: static;
    width: 1440px;
    height: 900px;
    left: 0px;
    top: 57px;
    overflow-x: scroll;
    background: #fcfcfc;
    margin: auto;
    /* box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25); */
  }

  .headline1 {
    position: static;
    height: 192px;
    /*  left: 0px;
    right: 0px; */
    top: 0px;
    font-family: Nunito;
    font-style: normal;
    font-weight: 800;
    font-size: 72px;
    line-height: 96px;
    display: flex;
    align-items: flex-end;
    letter-spacing: -1px;
    font-feature-settings: "pnum" on, "lnum" on;
  }

  p.author {
    font-size: 18px;
    line-height: 24px;
    margin-bottom: 4px;
  }

  p.date {
    font-size: 18px;
    line-height: 24px;
    margin-top: 4px;
    color: #858585;
  }
</style>
