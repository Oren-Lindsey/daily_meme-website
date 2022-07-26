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
        nodeRef.firstChild.style.cursor = 'pointer'
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
        nodeRef.firstChild.style.cursor = 'grab !important'
    }
    function startDrag(e) {
        nodeRef.firstChild.style.cursor = 'grabbing'
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
        nodeRef.firstChild.style.cursor = 'grab'
    }
    onMount(() => {
        window.localStorage.setItem('window-topLayer', 0)
    })
</script>
<div class="border rounded-none bg-gray-300 break-words resizable max-w-[100vw] min-w-[300px] min-h-fit w-fit absolute overflow-x-hidden" draggable={disabled} use:draggable={options} on:neodrag:start={(e) => startDrag(e)} on:neodrag:end={(e) => endDrag(e)} bind:this={nodeRef} title={title}>
    <div class="min-h-[30px] p-1 top-bar drag-handle overflow-x-hidden cursor-grab">
        <div class="absolute right-0 mr-2 z-[1000000000000]">
            <button class="button mt-[0.1vw] ml-[1px] cursor-pointer" title="Minimize window" on:click={minimize}><img class="h-[1.2vw]" src="https://canary---yellow.com/wp-content/themes/virgilabloh/images/icon-iconize.jpg" alt="Minimize window" /></button>
            <button class="button mt-[0.1vw] ml-[1px] cursor-pointer" title="Maximize window" on:click={maximize}><img class="h-[1.2vw]" src="https://canary---yellow.com/wp-content/themes/virgilabloh/images/icon-resize.jpg" alt="Maximize window" /></button>
            <button class="button mt-[0.1vw] ml-[1px] cursor-pointer" title="Close window" on:click={delElement}><img class="h-[1.2vw]" src="https://canary---yellow.com/wp-content/themes/virgilabloh/images/icon-close.jpg" alt="Close window" /></button>
        </div>
        <div class="break-words absolute text-left top-[8px] float-left w-full z-[1]">
            <p class="text-[white] mb-2 mt-[-3px]" style="font-size: 1.2vw">{title}</p>
        </div>
    </div>
    <div id="content" class="break-words p-2 overflow-x-hidden z-[10000000000000] cursor-auto text-center max-w-[80vw] min-w-fit grid place-items-center">
        <slot />
    </div>
</div>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Courier+Prime&display=swap');
    * {
        font-family: 'Courier Prime', monospace;
        overflow-x: hidden !important;
    }
    .top-bar {
        background-image: linear-gradient(90deg, rgba(51,78,165,1) 0%, rgba(76,127,193,1) 100%);
    }
    .resizable {
        resize:both;
        overflow:auto;
    }
    .border {
        border: 4px ridge #d8d8d8
    }
    .button {
        border: 1px outset #dad7d2
    }
</style>