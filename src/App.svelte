<script>
	import Cursor from './Cursor.svelte'
	import Target from './Target.svelte'
		import Nested from './Nested.svelte'

	let name = 'world';	import { writable } from 'svelte/store';

		import { setContext } from 'svelte';
  let activeCoords = writable(null)
	setContext('answer', activeCoords);
</script>

<Cursor snap={$activeCoords}/>

<Target/>
<Target/>

<Nested/>

<style>
	:root{
		cursor:none;
		background:#1A1A1A;
		
	}
</style>