<script context="module">
    export const prerender = true;
    import { page } from '$app/stores';
</script>
<svelte:window on:mousemove="{updateMouse}" />
<script>
    import { onMount } from 'svelte';
    import Window from '../components/Window.svelte'
    import Konami from '../components/Konami.svelte'
    import Ksg from '../components/Ksg.svelte'
    let konami = false
    let ksg = false
    let showGhost = false
    $: if (konami) {
        document.write(`<img src="https://alaska---alaska.com/wp-content/uploads/2020/01/not-seized.jpg" width=1000 class="w-screen min-w-screen" alt="This site has not been seized." />`)
    }
    $: if (ksg) {
        showGhost = true;
    }
    let mouseX = 0
    let mouseY = 0
    let time = new Date()
    async function updateMouse(e) {
        mouseX = e.clientX
        mouseY = e.clientY
    }
    $: currenttime = time.toLocaleString()
    setInterval(() => {
        time = new Date()
    }, 1000)
    let gpuAcceleration = true
    onMount(async () => {
        loaded = true
    })
</script>
<noscript>
    <h1 class="text-white text-3xl text-center shadow-lg">Please enable javascript to fully experience this site</h1>
</noscript>
<div class="desktop">
<Konami bind:konami />
<Ksg bind:ksg />
<Window title="stats.app" x=60 y=70 gpuAcceleration={gpuAcceleration}>
    <div class="inline text-center">
        Mouse X: <code>{mouseX}</code>
        <br>
        Mouse Y: <code>{mouseY}</code>
        <br>
        Time: <code>{currenttime}</code>
        <br>
        Current URL: <code>{$page.url.href}</code>
        <br>
        GPU Acceleration: <code>{gpuAcceleration}</code>
    </div>
</Window>
<Window title="about.txt - editor" x=200 y=100 gpuAcceleration={gpuAcceleration}>
    <textarea id="textarea" class="bg-transparent box-border font-sans min-w-max w-full h-72 m-0 p-2">Hi, I'm Oren. I'm a full stack web developer (sveltekit ftw!) and I live in North Carolina (it's the best state)</textarea>
</Window>
<Window title="coding projects" x=100 y=450 gpuAcceleration={gpuAcceleration}>
    <ul class="grid grid-cols-1 place-items-center">
        <li>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://list.lindsey.studio"><code>list-v2</code> - a wishlist website</a>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey/list-v2"><img loading=lazy class="inline" src="/GitHub-Mark-32px.png" width=16 alt="github logo" /></a>
        </li>
        <li>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://quack.lindsey.studio"><code>Quack</code> - share and answer questions</a>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey/quack"><img loading=lazy class="inline" src="/GitHub-Mark-32px.png" width=16 alt="github logo" /></a>
        </li>
        <li>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey/wasteof-client3"><code>wasteof-client</code> - npm package for wasteof.money</a>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey/wasteof-client3"><img loading=lazy class="inline" src="/GitHub-Mark-32px.png" width=16 alt="github logo" /></a>
        </li>
        <li>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://lindsey.studio"><code>lindsey.studio</code> - this website</a>
            <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey/lindsey.studio"><img loading=lazy class="inline" src="/GitHub-Mark-32px.png" width=16 alt="github logo" /></a>
        </li>
    </ul>
    <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey">View all of my coding projects</a>
</Window>
<Window title="contact" x=220 y=650 gpuAcceleration={gpuAcceleration}>
    <table class="table-auto w-full rounded-[5px]">
        <caption class="m-1">How to contact me</caption>
        <thead class="bg-gray-300 rounded-[5px]"><tr><td class="text-center">site</td><td class="text-center">username</td></tr></thead>
        <tbody>
            <tr class="transition ease-in-out delay-75"><td><a class="text-center decoration underline-offset-1 hover:underline inline m-1" href="https://wasteof.money/@ee">wasteof.money</a></td><td class="text-center">@ee</td></tr>
            <tr class="transition ease-in-out delay-75"><td><a class="text-center decoration underline-offset-1 hover:underline inline m-1" href="https://scratch.mit.edu/users/scratchusername40">scratch</a></td><td class="text-center">@scratchusername40</td></tr>
            <tr class="transition ease-in-out delay-75"><td><a class="text-center decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey">github</a></td><td class="text-center">Oren-Lindsey</td></tr>
            <tr class="transition ease-in-out delay-75"><td><a class="text-center decoration underline-offset-1 hover:underline inline m-1" href="https://www.npmjs.com/~orenlindsey">npm</a></td><td class="text-center">orenlindsey</td></tr>
            <tr class="transition ease-in-out delay-75"><td><a class="text-center decoration underline-offset-1 hover:underline inline m-1" href="https://replit.com/@s40">replit</a></td><td class="text-center">@s40</td></tr>
            <tr class="transition ease-in-out delay-75"><td><a class="text-center decoration underline-offset-1 hover:underline inline m-1" href="https://www.guilded.gg/profile/mpQPDENA">guilded</a></td><td class="text-center">@e</td></tr>
        </tbody>
        <style>
            tbody tr:hover {
                background-color: rgb(229 231 235 / 1);
            }
        </style>
    </table>
</Window>
</div>
<div class="mobile w-full">
    <Window x=0 y=0 gpuAcceleration={gpuAcceleration} title="about.txt" disabled>
        <p>Hi, I'm Oren. I'm a full stack web developer (sveltekit ftw!) and I live in North Carolina (it's the best state)</p>
        <a class="decoration underline-offset-1 hover:underline inline m-1" href="https://github.com/oren-lindsey">See all of my coding projects on GitHub</a>
    </Window>
    <img src="/kidsseeghosts.png" alt="kids see ghosts" width=100  class="absolute bottom-[12%] right-[30%] z-[20000000000000000000000000000000000000000000000000000000000000000000000000000000000000]" />
</div>
{#if showGhost}
<img src="/kidsseeghosts.png" alt="kids see ghosts" width=100  class="absolute bottom-[15%] right-[12%] z-[20000000000000000000000000000000000000000000000000000000000000000000000000000000000000]" />
{/if}
<style>
    #textarea::-webkit-resizer {
        background-color: transparent
    }
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
</style>