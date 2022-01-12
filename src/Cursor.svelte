<script>
  import { tweened } from "svelte/motion";
  import { quadIn } from "svelte/easing";
  let x, y;
  let cursorType = null;
  export let snap;
  let m = { x: 0, y: 0 };

  $: cursorX = m.x;
  $: cursorY = m.y;
</script>

<svelte:window
  on:mousemove={(e) => {
    m.x = e.clientX;
    m.y = e.clientY;
  }}
/>

<br />

<div
  class="cursor"
  class:snap
  style="transform:translate( calc({snap
    ? snap.x
    : cursorX}px - 50%) ,calc({snap ? snap.y : cursorY}px - 50%))"
/>
{#key cursorType}
  {#if cursorType > -1}
    <div
      class="snap-cursor-{cursorType}"
      class:snap
      style="transform:translate( calc({!snap
        ? -10000
        : cursorX}px - 50%) ,calc({!snap ? -10000 : cursorY}px - 50%))"
    />
  {/if}
{/key}
<!-- <div
    class="snap-cursor-0"
	class:snap
    style="transform:translate( calc({!snap
		? -10000
		: cursorX}px - 50%) ,calc({!snap ? -10000 : cursorY}px - 50%))"
  /> -->

<!-- <div class="snap-debug"  style="transform:translate({snap?snap.x:0}px,{snap?snap.y:0}px)">
	<div class="pos-debug"  style="transform:translate({$x}px,{$y}px)"></div>
	
</div> -->
<div>
  <label>
    <input
      type="radio"
      bind:group={cursorType}
      name="cursorType"
      value={null}
    />
    No inner cursor
  </label>

  <label>
    <input type="radio" bind:group={cursorType} name="cursorType" value={0} />
    inner 1
  </label>

  <label>
    <input type="radio" bind:group={cursorType} name="cursorType" value={1} />
    inner 2
  </label>
</div>

<style>
	label{
		color:white;
		/* cursor:none; */
	}
  .snap-cursor-0 {
    position: fixed;
    width: 15px;
    height: 15px;
    top: 0;
    left: 0;

    background: #eeff00;
    pointer-events: none;

    border-radius: 50%;
    opacity: 0;
    transition: opacity 250ms ease-in-out 250ms;
  }
  .snap-cursor-0.snap {
    opacity: 0.5;
  }
  .snap-cursor-1 {
    position: fixed;
    width: 30px;
    height: 30px;
    top: 0;
    left: 0;
    border: #ffffffff solid thin;
    border-radius: 50%;
    background: #eeff0000;
    pointer-events: none;

    transition: width 150ms ease-in, height 150ms ease-in,
      background 150ms ease-in, border 150ms ease-in;
  }
  .snap-cursor-1.snap {
    width: 15px;
    height: 15px;
    background: #eeff0080;
    pointer-events: none;
    border: #ffffff00 solid thin;
  }
  .snap-debug {
    position: fixed;
    top: 0;
    left: 0;
    width: 4px;
    height: 4px;
    border: green solid thin;
  }
  .pos-debug {
    position: fixed;
    top: 0;
    left: 0;
    width: 4px;
    height: 4px;
    border: blue solid thin;
  }
  .cursor {
    position: fixed;
    top: 0;
    left: 0;
    width: 30px;
    height: 30px;
    border: #ffffff solid thin;
    border-radius: 50%;
    pointer-events: none;
    transition: width 150ms ease-in, height 150ms ease-in, border 150ms ease-in;
  }
  .cursor.snap {
    transition: width 150ms ease-in, height 150ms ease-in, border 150ms ease-in,
      transform 150ms ease-in;
    width: 60px;
    height: 60px;
    border: #eeff00 solid thin;
  }
</style>
