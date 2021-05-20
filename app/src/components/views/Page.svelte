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

<!-- BACKGROUND IMG PRE-LOADER -->
<div id="preload">
  <!-- svelte-ignore a11y-missing-attribute -->
  <img
    src="https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/public/img/heroBackground.svg"
  />
</div>

<!-- HERO -->
<div class="hero">
  <div class="heroText">
    <!-- Headline without animation -->
    <!-- <p class="headline1">
      How we ask Google for <span style="color:#ED715D">help?</span>
    </p> -->

    <div class="typewriter">
      <p>
        How we ask Google for <span style="color:#ED715D">help?</span>
      </p>
    </div>

    <p class="author">
      By <span style="font-weight:600">Xavier Bolló, Sara Chodosh</span> and
      <span style="font-weight:600">Santiago Salcido</span>
    </p>
    <p class="date">May 19, 2021</p>
  </div>
</div>

<!-- CONTENT -->
<!-- <div class="contentWrapper">
  <p class="lead">
    Asking for help is one of the hardest things to do. But asking Google is
    easy.
  </p>
</div> -->

<!-- PARALLAX SLIDES -->

<Parallax
  sections="2"
  style="background-color: 
  background: rgb(197,202,233);
background: linear-gradient(180deg, rgba(197,202,233,1) 0%, rgba(0,40,105,1) 70%);"
  bind:this={parallax}
>
  <ParallaxLayer
    offset="1"
    rate="1"
    style="background-color: 
  background: rgb(197,202,233);
background: linear-gradient(0deg, rgba(197,202,233,1) 0%, rgba(0,40,105,1) 100%);"
  />
  <ParallaxLayer offset="2" rate="1" style="background-color: #C5CAE9;" />

  <ParallaxLayer
    offset="0"
    rate="1"
    span="3"
    style="background-image: {url('stars', true)}; background-size: cover;"
  />

  <!-- TEXT BOX 1 -->
  <ParallaxLayer offset="0.3" rate=".5" span="1">
    <div class="textBox">
      <p class="pTextBox">
        Asking for help is one of the <b>hardest</b> things to do. But asking Google
        is easy.
      </p>
    </div>
  </ParallaxLayer>

  <!-- TEXT BOX 2 -->

  <ParallaxLayer
    offset=".4"
    rate="0.2"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img
      src={"https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/public/img/bee1.svg"}
      alt="bee"
      style="width: 15%; margin-right: 75%;"
    />
  </ParallaxLayer>

  <ParallaxLayer
    offset=".2"
    rate="0.2"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img
      src={"https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/public/img/bee2.svg"}
      alt="bee"
      style="width: 8%; margin-left: 75%;"
    />
  </ParallaxLayer>

  <ParallaxLayer
    offset=".7"
    rate="0.3"
    style="display: flex; align-items: center; justify-content: center;"
  >
    <img
      src={"https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/public/img/bee2.svg"}
      alt="bee"
      style="width: 25%; margin-left: 50%;"
    />
  </ParallaxLayer>

  <ParallaxLayer offset=".9" rate=".5" span="1">
    <div class="textBox">
      <p class="pTextBox">
        Over the years, we’ve asked Google for help with a lot of things—about
        <a
          href="https://trends.google.com/trends/explore?q=bees"
          target="_blank">bees</a
        >, for example, but also
        <a
          href="https://trends.google.com/trends/explore?q=hoarding"
          target="_blank">hoarding</a
        >
        and
        <a
          href="https://trends.google.com/trends/explore?q=floods"
          target="_blank">floods</a
        >—and the beauty of the resulting data is that it reveals what we are
        most private about asking. To reach out to a friend to get help with
        alcoholism or to offer support for someone struggling with grief is to
        be vulnerable.
        <b>What you ask Google stays between you and Google.</b>
      </p>
    </div>
  </ParallaxLayer>

  <!-- TEXT BOX 3 -->
  <ParallaxLayer offset="1.3" rate=".5" span="1">
    <div class="textBox">
      <p class="pTextBox">
        In the midst of the pandemic, conversations about mental health have
        emerged in the media. But <b>Google Trends data</b> shows that we were always
        dealing with these issues—it’s just that no one was talking to each other
        about it.
      </p>
    </div>
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
      style="display: block; width: 25%; margin-left: 32%;"
    />
    <img
      src={url("cloud")}
      alt=""
      style="display: block; width: 10%; margin-left: 80%;"
    />
  </ParallaxLayer>


</Parallax>

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
  <p class="subtitle">
    Index A | Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  </p>
  <img src="img/heatMapA.png" alt="heatMapA" width="100%" height="auto" />
  <p class="subtitle">
    Index B | Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  </p>
  <img src="img/heatMapB.png" alt="heatMapB" width="100%" height="auto" />
  <p />
</div>

<!-- CSS & STYLES -->
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

  #preload {
    display: none;
  }

  .hero {
    margin: auto;
    position: static;
    max-width: 1440px;
    height: 1400px;
    overflow-x: visible;
    background-size: cover;
    background-position: center -40px;
    background-image: url("https://github.com/sarachodosh/mvtec-google-workshop/raw/santiago/app/public/img/heroBackground.svg");
  }

  .heroText {
    max-width: 880px;
    padding-top: 120px;
    margin: auto;
    position: static;
    height: 500px;
    left: 0px;
    top: 57px;
    overflow-x: scroll;
  }

  p.author {
    font-size: 18px;
    line-height: 24px;
    margin-bottom: 8px;
    color: #ffffff;
    margin: auto;
    padding-top: 30px;
    text-align: center;
  }

  p.date {
    font-size: 16px;
    line-height: 24px;
    padding-top: 8px;
    color: #c5cae9;
    margin: auto;
    text-align: center;
  }

  p {
    margin-top: 24px;
    margin-bottom: 24px;
  }

  .contentWrapper {
    max-width: 800px;
    /* border-top: 5px solid #002869; */
    margin: auto;
    /* margin-top: 64px; */
    padding: 48px;
    background-color: #ffffff;
    box-shadow: 0px 8px 0px #002869;
  }

  .textBox {
    max-width: 800px;
    margin: auto;
    padding: 48px;
    background-color: #ffffff;
    box-shadow: 0px 8px 0px #002869;
  }

  .subtitle {
    font-size: 16px;
    font-weight: 600;
    line-height: 160%;
    margin-top: 32px;
    margin-bottom: 8px;
  }

  .pTextBox {
    font-family: "Nunito", sans-serif;
    font-style: normal;
    font-weight: 400;
    font-size: 24px;
    line-height: 160%;
    margin-top: 0px;
    margin-bottom: 0px;
  }

  /*   .lead {
    font-family: "Nunito", sans-serif;
    font-style: normal;
    font-weight: 800;
    font-size: 24px;
    line-height: 160%;
    margin-top: 0px;
    margin-bottom: 0px;
  } */
  .sectionsComp {
    justify-content: left;
    flex-direction: column;
    align-items: left;
    margin: auto;
    display: flex;
    padding: 0px 0px 24px 0px;
  }
  h2 {
    /* margin: 32px 0px 0px 0px; */
    line-height: 48px;
    font-weight: 600;
    /* font-size: 48px; */
    /* border-top: 2px solid #bdbdbd; */
    /* padding-top: 32px; */
    font-family: "Nunito", sans-serif;
  }

  /* Typing animation */
  .typewriter p {
    color: #f1f1f1;
    font-size: 64px;
    font-family: "Nunito", sans-serif;
    font-weight: 800;
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
