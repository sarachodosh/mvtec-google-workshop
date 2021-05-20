<!-- scripts and imports -->
<script>
  import { Parallax, ParallaxLayer } from "svelte-parallax";

    import Joyplot from '../charts/Joyplot.svelte';
    import CirclePacking from '../charts/CirclePacking.svelte';

    import { format, precisionFixed } from 'd3-format';

    import dataA from '../../data/dataA_long.csv';
	  import dataB from '../../data/dataB_long.csv';
    import dataG from '../../data/dataG.csv';
    import { curveCatmullRom } from 'd3-shape';



  let parallax;
  let disabled = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  const url = (name, wrap = false) =>
    `${
      wrap ? "url(" : ""
    }https://awv3node-homepage.surge.sh/build/assets/${name}.svg${
      wrap ? ")" : ""
    }`;


</script>

<!-- HERO -->
<div class="hero">
  <div class="heroText">
    <!-- Headline without animation -->
    <!-- <p class="headline1">
      How we ask Google for <span style="color:#ED715D">help?</span>
    </p> -->

    <div class="typewriter">
      <h1>
        How we ask Google for <span style="color:#ED715D">help?</span>
      </h1>
    </div>



    <p class="author">
      By <span style="font-weight:600">Xavier Bolló, Sara Chodosh</span> and
      <span style="font-weight:600">Santiago Salcido</span>
    </p>
    <p class="date">May 19, 2021</p>
  </div>
</div>

<!-- OLD IDEA with the search bar, erase before final commit -->
<!-- <p align="center">
  <img
    src="https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/src/img/searchImg.png"
    alt="search"
    width="1000"
    height="auto"
    style="
    padding-bottom: 60px;
"
  />
</p> -->

<!-- CONTENT -->
<div class="contentWrapper">
  <p class="lead">
    Asking for help is one of the hardest things to do. But asking Google is
    easy.
  </p>
  <p class="lead">
    Over the years, we’ve asked Google for help with a lot of things—about bees,
    for example, but also hoarding and floods—and the beauty of the resulting
    data is that it reveals what we are most private about asking. To reach out
    to a friend to get help with alcoholism or to offer support for someone
    struggling with grief is to be vulnerable. What you ask Google stays between
    you and Google.
  </p>
  <p>
    In the midst of the pandemic, conversations about mental health have emerged
    in the media. But Google Trends data shows that we were always dealing with
    these issues—it’s just that no one was talking to each other about it.
  </p>
</div>

<!-- CHART 1 -->
<div class="contentWrapper">
  <div class="sectionsComp">
    <h2>Mental health issues dominate searches</h2>
  </div>
  <p>
    Searches for “how to help _____” or “how to help someone with _____” are
    consistently dominated by mental health issues.
  </p>
  <CirclePacking 
    data={dataG}
  />
</div>

<!-- <p align="center">
  <iframe
    width="70%"
    height="382"
    frameborder="0"
    src="https://observablehq.com/embed/@sechodosh/google-trends?cells=beeswarm"
    style="align=center"
  />
</p> -->

<!-- CHART 2 -->
<div class="contentWrapper">
  <div class="sectionsComp">
    <h2>Sudden tragedies draw our attention, but not for long</h2>
  </div>
  <p>
    There are blips where natural disasters strike—a flood, a hurricane—or
    during political upheaval and other crises. But these abstract tragedies
    don’t capture our attention for long. Their peaks rise and fall again
    quickly. Meanwhile, interest in the everyday tragedies that strike us and
    our loved ones, from depression to anorexia, stays fairly high.
  </p>
  <p>
    Interest in some of these has risen sharply in the last year—rape, anger
    management, and anxiety, to name a few. Others have seen a steady rise.
    Perhaps no topic has been of as much interest, though, as depression.
  </p>
  <Joyplot
  data={dataB}
  options={
      {
    curve: curveCatmullRom,
          layout: 'col',
          format: format
      }
  }
/>
</div>
<!-- <p align="center">
  <iframe
    width="70%"
    height="382"
    frameborder="0"
    src="https://observablehq.com/embed/@sechodosh/google-trends?cells=beeswarm"
    style="align=center"
  />
</p> -->

<!-- CHART 3 -->
<div class="contentWrapper">
  <div class="sectionsComp">
    <h2>Depression is consistently one of our top concerns</h2>
  </div>
  <p>
    It took a global pandemic to overtake the top spot from depression, and even
    the interest in that waned fairly quickly. For now, these searches are
    between us and the Google search bar. But if the coronavirus teaches us
    anything, it should be that we need to lean on each other—we’re all
    searching for help about the same things.
  </p>
  <img src="img/heatMapA.png" alt="heatMapA" width="100%" height="auto" />
  <img src="img/heatMapB.png" alt="heatMapB" width="100%" height="auto" />
  <p />
</div>

<!-- TEST import local images -->
<!-- <img src="img/circlePacking.png" alt="background image" /> -->

<!-- ASK XAVI IF I CAN ERASE THIS -->
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

<!-- PARALLAX TEMPLATE -->
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

<!-- CSS & STYLE -->
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
    margin: auto;
    position: static;
    max-width: 1440px;
    height: 1496px;
    overflow-x: visible;
    background-size: cover;
    background-position: center top;
    background-image: url("https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/public/img/heroBackground.svg");
  }

  .heroText {
    max-width: 680px;
    padding-top: 120px;
    margin: auto;
    position: static;
    height: 500px;
    left: 0px;
    top: 57px;
    overflow-x: scroll;
  }

  .headline1 {
    font-family: Nunito;
    font-style: normal;
    font-weight: 800;
    font-size: 72px;
    line-height: 96px;
    color: #ffffff;
    letter-spacing: -1px;
    font-feature-settings: "pnum" on, "lnum" on;
  }

  h1 {
    font-family: Nunito;
    font-style: normal;
    font-weight: 800;
    font-size: 72px;
    line-height: 96px;
    color: #ffffff;
    letter-spacing: -1px;
    font-feature-settings: "pnum" on, "lnum" on;
  }

  p.author {
    font-size: 18px;
    line-height: 24px;
    margin-bottom: 8px;
    color: #ffffff;
  }

  p.date {
    font-size: 16px;
    line-height: 24px;
    margin-top: 4px;
    color: #c5cae9;
  }

  p {
    margin-top: 24px;
    margin-bottom: 24px;
  }

  .contentWrapper {
    max-width: 776px;
    margin: auto;
    padding: 48px;
    background-color: #ffffff;
  }

  .lead {
    font-family: Nunito;
    font-style: normal;
    font-weight: 800;
    font-size: 20px;
    line-height: 160%;
  }
  .sectionsComp {
    justify-content: left;
    flex-direction: column;
    align-items: left;
    margin: auto;
    display: flex;
    padding: 64px 0px 32px 0px;
  }
  h2 {
    margin: 32px 0px 0px 0px;
    line-height: 48px;
    font-weight: 600;
    /* font-size: 48px; */
    border-top: 2px solid #bdbdbd;
    padding-top: 32px;
    font-family: "Nunito";
  }

  /* Typing animation */
  .typewriter h1 {
    color: #f1f1f1;
    overflow: hidden; /* Ensures the content is not revealed until the animation */
    border-right: 0.15em solid #ed715d; /* The typwriter cursor */
    white-space: nowrap; /* Keeps the content on a single line */
    margin: 0 auto; /* Gives that scrolling effect as the typing happens */
    letter-spacing: -0.02em; /* Adjust as needed */
    animation: typing 2.5s steps(30, end), blink-caret 0.5s step-end infinite;
  }

  /* The typing effect */
  @keyframes typing {
    from {
      width: 0;
    }
    to {
      width: 100%;
    }
  }

  /* The typewriter cursor effect */
  @keyframes blink-caret {
    from,
    to {
      border-color: transparent;
    }
    50% {
      border-color: #ed715d;
    }
  }

  /* Medium devices (landscape tablets, 768px and up) */
  @media only screen and (min-width: 768px) {
    .hero {
      width: 100%;
    }
  }
</style>
