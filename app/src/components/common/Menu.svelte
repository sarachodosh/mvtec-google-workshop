<script>
    import Tweet from "./Tweet.svelte";
</script>

<div class="navbar">
    <!-- <menu> -->
        
    <button
    
        class="icon"
        on:click={() => window.open()}
        target="_blank"
        role="link"
        rel="noopener"
        aria-label="Find this repo on GitHub (Opens in a new tab)">
        <svg
            role="img"
            aria-roledescription="logo"
            aria-label="GitHub logo"
            viewBox="0 0 48 48"
            width="24"
            height="24"
            color="#ffffff"
            ><path
                d="M32,16c-8.8,0-16,7.2-16,16c0,7.1,4.6,13.1,10.9,15.2 c0.8,0.1,1.1-0.3,1.1-0.8c0-0.4,0-1.4,0-2.7c-4.5,1-5.4-2.1-5.4-2.1c-0.7-1.8-1.8-2.3-1.8-2.3c-1.5-1,0.1-1,0.1-1 c1.6,0.1,2.5,1.6,2.5,1.6c1.4,2.4,3.7,1.7,4.7,1.3c0.1-1,0.6-1.7,1-2.1c-3.6-0.4-7.3-1.8-7.3-7.9c0-1.7,0.6-3.2,1.6-4.3 c-0.2-0.4-0.7-2,0.2-4.2c0,0,1.3-0.4,4.4,1.6c1.3-0.4,2.6-0.5,4-0.5c1.4,0,2.7,0.2,4,0.5c3.1-2.1,4.4-1.6,4.4-1.6 c0.9,2.2,0.3,3.8,0.2,4.2c1,1.1,1.6,2.5,1.6,4.3c0,6.1-3.7,7.5-7.3,7.9c0.6,0.5,1.1,1.5,1.1,3c0,2.1,0,3.9,0,4.4 c0,0.4,0.3,0.9,1.1,0.8C43.4,45.1,48,39.1,48,32C48,23.2,40.8,16,32,16z"
            /></svg
        >
    </button>
    <div class="navbarTitle">The blues of a pandemic</div>
    <Tweet tweet="Check this " url="https://www.google.com/" />
    
    <!-- </menu> -->
</div>

<style>
    .navbar {
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        justify-content: center;
        align-items: center;
        padding: 8px 16px 8px 8px;
        color: #ffffff;
        font-family: "Nunito", sans-serif;
        text-transform: uppercase;
        background-color: #01609a;
        height: 48px;
    }

    .navbarTitle {
        text-align: center;
        vertical-align: middle;
        width: 100%;
    }
</style>
