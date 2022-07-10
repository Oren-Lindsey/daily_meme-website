<svelte:window on:keyup="{combinator}" />

<script>
	export let ksg = false
	
	let combo = []
	let time = Date.now()
	
	function combinator({ keyCode }) {
		const list = [75, 83, 71, 32]
		const now = Date.now()
		
		if (!list.includes(keyCode)) return
		if (now - time > 2000) combo = []
		
		combo.push(keyCode)
		time = now
		console.log(combo)
		if (JSON.stringify(combo) === JSON.stringify(list)) {
			ksg = !ksg
		}
	}
</script>