<script context="module">
    export const prerender = true;
</script>
<script>
    import { MetaTags } from 'svelte-meta-tags';
    import Window from '../components/Window.svelte'
    let gpuAcceleration = true
</script>
<noscript>
    <h1 class="text-white text-3xl text-center shadow-lg">Please enable javascript to fully experience this site</h1>
</noscript>
<div class="desktop">
    <div class="absolute bg-[#018281] left-0 top-0 h-screen max-h-screen overflow-hidden w-[124px] window-border">
        <p class="text-center text-white text-xl mono-font">Links</p>
    </div>
    <a href="https://wasteof.money/@daily_meme"><img src="https://wasteof.money/brand/nav-logo.svg" alt="My pfp" title="My pfp" class="absolute top-[20px] left-0 m-[10px] w-[100px]" /></a>
    <Window x=20 y=100 gpuAcceleration={gpuAcceleration} title="About me" disabled=false><p>Hi I'm daily_meme i'm a 13 year old boy who likes to post memes and do graphic design stuff and i like to sleep (sometimes)</p></Window>
    <Window x=200 y=300 gpuAcceleration={gpuAcceleration} title="Pictures" disabled=false><p class="grid place-items-center">Pictures here</p></Window>
    <Window x=400 y=500 gpuAcceleration={gpuAcceleration} title="ratio" disabled=false>
        <p class="text-xl">Ratio</p>
        <a href="https://wasteof.money/@ratio"><img src="https://beta.wasteof.money/users/ratio/picture" class="h-[100px]" alt="ratio's pfp" /></a>
    </Window>
</div>
<div class="mobile w-full">
    <Window x=0 y=0 gpuAcceleration={gpuAcceleration} title="Daily Meme" disabled=false><p>:P</p></Window>
</div>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Courier+Prime&display=swap');
    @media (max-width: 640px) {
        .desktop {
            display: none !important;
        }
        .mobile {
            display: block !important;
        }
    }
    @media (min-width: 640px) {
        .mobile {
            display: none !important;
        }
        .desktop {
            display: block !important;
        }
    }
    .mono-font {
        font-family: 'Courier Prime', monospace;
    }
    .window-border {
        border-right: 4px ridge #d8d8d8
    }
</style>
<MetaTags
  title="daily_meme"
  description="daily_meme's website"
  openGraph={{
    type: 'website',
    title: 'daily_meme',
    description: `daily_meme's website`,
    site_name: 'daily_meme',
  }}
  twitter={{
    cardType: 'summary_large_image',
    title: 'daily_meme',
    description: `daily_meme's website`
  }}
/>