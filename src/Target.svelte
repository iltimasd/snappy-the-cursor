<script>
	let targetCoord;
		import { getContext } from 'svelte';
 let down;
	const answer = getContext('answer');
</script>
<div class="target" class:down
		 on:mouseenter={()=>{
	$answer = {y:targetCoord.getBoundingClientRect().top,
						x:targetCoord.getBoundingClientRect().left}
	}}
	on:mouseleave={()=>{
	$answer = null;
	down=false;
	}}
	on:mousedown={()=>{
		down=true;
	}}
	on:mouseup={()=>{
		down=false;
	}}
	>
	<div class="ploss" >
		<div class:down>
			
		<div class="ploss-bar">
		</div>
		<div class="ploss-bar updown">
		</div>
		<div id="center-ref" bind:this={targetCoord}/>
		</div>
	</div>
</div>

<style>
	#center-ref{
		position:absolute;
		left:calc(50% - 0px);
		top:calc(50% - 1px);
		width:1px;
		height:0px;
/* 		border-top: red solid thin; */
	}
	.target{
		position:relative;
		width:75px;
		height:75px;
/* 		border: red solid thin; */
		border-radius: 50%;
		transition:transform 350ms ease-in-out
	}
	.target:hover{
/* 				border: green solid thin; */
				transform:rotate(45deg);
	}
	.ploss{
		position:absolute;
		left:50%;
		top:50%;
		transform:translate(-50%,0px);
	}
	.down{
				transform:translate(1px,1px);

	}

	.ploss-bar{
		position:relative;
		top:50%;
		left:0px;
		width:40px;
		border-top: white solid thin;
	}
	.target:hover .ploss-bar{
			border-top: #EEFF00 solid thin;
	}
	
	.updown{
		transform:rotate(90deg);
	}
</style>