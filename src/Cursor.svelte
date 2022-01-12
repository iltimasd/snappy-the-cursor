<script>
	  import { tweened } from "svelte/motion";
  import { quadIn } from "svelte/easing";
 let x,y;
	export let snap;
	let m={x:0,y:0}

	$: cursorX=  m.x;
	$: cursorY=  m.y;
	
</script>


<svelte:window on:mousemove={(e)=>{m.x=e.clientX;m.y=e.clientY}}></svelte:window>


<br>


<div class="cursor" class:snap
		 style="transform:translate( calc({snap?snap.x:cursorX}px - 50%) ,calc({snap?snap.y:cursorY}px - 50%))">
</div>

<!-- <div class="snap-debug"  style="transform:translate({snap?snap.x:0}px,{snap?snap.y:0}px)">
	<div class="pos-debug"  style="transform:translate({$x}px,{$y}px)"></div>
	
</div> -->
<style>
	.snap-debug{
				position:fixed;
top:0;
		left:0;
			width:4px;
		height:4px;
		border: green solid thin;
	}
		.pos-debug{
				position:fixed;
top:0;
		left:0;
			width:4px;
		height:4px;
		border: blue solid thin;
	}
	.cursor{
		position:fixed;
		top:0;
		left:0;
		width:30px;
		height:30px;
		border: #ffffff solid thin;
		border-radius: 50%;
		pointer-events:none;
		transition: width 150ms ease-in, height 150ms ease-in, border 150ms ease-in;
	}
	.snap{
		transition:  width 150ms ease-in, height 150ms ease-in, border 150ms ease-in, transform 150ms ease-in;
		width:60px;
		height:60px;
		border: #EEFF00 solid thin;

	}
</style>