<script>
    import {onMount} from 'svelte'
    import { draggable } from '@neodrag/svelte';
    export let title
    export let x
    export let y
    export let gpuAcceleration
    export let disabled
    let maximized = false
    let layer = 1
    let defaultPos = {x: x, y: y}
    let options = { gpuAcceleration: gpuAcceleration, position: defaultPos, defaultPosition: defaultPos, disabled: disabled, bounds: { left: 0, top: 0, bottom: 0, right: 0 }, handle: '.drag-handle' }
    let nodeRef
    function delElement() {
        nodeRef.parentNode.removeChild(nodeRef)
    }
    function maximize(e) {
        maximized = true
        nodeRef.classList.add('min-w-[100vw]')
        nodeRef.classList.add('min-h-[100vh]')
        nodeRef.classList.remove('min-w-[300px]')
        nodeRef.classList.remove('min-h-fit')
        nodeRef.classList.add('w-screen')
        nodeRef.classList.add('h-screen')
        nodeRef.style.transform = `rotate(7deg)`
        nodeRef.classList.add('z-[10000000000000000000000000000000000000000000000000000000000000000000000000000000000000]')
        options = { gpuAcceleration: true, defaultPosition: defaultPos, position: {x: 0, y: 0}, handle: '.drag-handle' }
        e.target.setAttribute('draggable', 'false')
        options = { gpuAcceleration: gpuAcceleration, position: {x:0, y:0}, defaultPosition: defaultPos, disabled: true, bounds: { left: 0, top: 0, bottom: 0, right: 0 }, handle: '.drag-handle' }
        e.target.style.cursor = 'pointer'
    }
    function minimize(e) {
        nodeRef.classList.remove('min-w-[100vw]')
        nodeRef.classList.remove('min-h-[100vh]')
        nodeRef.classList.add('min-w-[300px]')
        nodeRef.classList.add('min-h-fit')
        nodeRef.classList.remove('h-screen')
        nodeRef.classList.remove('w-screen')
        nodeRef.classList.remove('z-[10000000000000000000000000000000000000000000000000000000000000000000000000000000000000]')
        if (maximized == true) {
            options = { gpuAcceleration: gpuAcceleration, position: defaultPos, defaultPosition: defaultPos, disabled: disabled, bounds: { left: 0, top: 0, bottom: 0, right: 0 }, handle: '.drag-handle' }
        } else {
            options = { gpuAcceleration: gpuAcceleration, defaultPosition: defaultPos, disabled: disabled, bounds: { left: 0, top: 0, bottom: 0, right: 0 }, handle: '.drag-handle' }
        }
        maximized = false
        e.target.style.cursor = 'grab'
    }
    function startDrag(e) {
        e.target.style.cursor = 'grabbing'
        let topLayer = localStorage.getItem('window-topLayer')
        if (topLayer !== null) {
            topLayer = parseInt(topLayer)
        }
        if (topLayer == null || typeof topLayer !== 'number' || topLayer === NaN || topLayer === undefined) {
            localStorage.setItem('window-topLayer', layer)
            topLayer = 1
        }
        const newLayer = topLayer + 1
        e.target.style.zIndex = newLayer
        layer = newLayer
        localStorage.setItem('window-topLayer', layer)
    }
    function endDrag(e) {
        e.target.style.cursor = 'grab'
    }
    onMount(() => {
        window.localStorage.setItem('window-topLayer', 0)
    })
</script>
<div class="cursor-grab rounded-[5px] bg-[#ececec] break-words window-shadow resizable max-w-[100vw] min-w-[300px] min-h-fit absolute" draggable={disabled} use:draggable={options} on:neodrag:start={(e) => startDrag(e)} on:neodrag:end={(e) => endDrag(e)} bind:this={nodeRef}>
    <div class="w-full rounded-t-[5px] top-[5px] bottom-[5px] left-[6px] pt-1 bg-gray-500 top-bar flex align-items-start drag-handle">
        <button title="Close window" class="bg-[#ff5f58] border-[#e1483f] m-1 mb-2 ml-2 h-[12px] w-[12px] rounded-full border-solid border cursor-pointer inline z-10 active:bg-[#bf4942]" on:click={delElement}></button>
        <button title="Minimize window" class="bg-[#ffbe2f] border-[#e0a028] m-1 mb-2 h-[12px] w-[12px] rounded-full border-solid border cursor-pointer inline z-10 active:bg-[#bf8e22]" on:click={minimize}></button>
        <button title="Maximize window" class="bg-[#2ac940] border-[#2bac2d] m-1 mb-2 h-[12px] w-[12px] rounded-full border-solid border cursor-pointer inline z-10 active:bg-[#1d9730]" on:click={maximize}></button>
        <div class="absolute grid place-items-center w-full z-[1]">
            <p class="text-[#423f42] mb-2 mt-[-3px]">{title}</p>
        </div>
    </div>
    <div id="content" class="break-words grid place-items-center p-2">
        <slot />
    </div>
</div>
<style>
    .top-bar {
        background-image: linear-gradient(180deg,#e7e6e7,#d1d0d1);
        box-shadow: inset 0 0 0 0 hsla(0,0%,100%,.6),inset 0 0 0 0 rgba(0,0,0,.2)
    }
    .window-shadow {
        box-shadow: 0 0 1px 0 rgba(0,0,0,.9),0 20px 30px 0 rgba(0,0,0,.3),0 10px 50px 0 rgba(0,0,0,.2)
    }
    .resizable {
        resize:both;
        overflow:auto;
    }
    *::-webkit-resizer {
        background-color: transparent
    }
</style>