<script lang="ts">
 import { onMount } from 'svelte';
//  let count: number = 0
//  const increment = () => {
//    count += 1
//  }
let canvaszoom;
let ctx;
let canvas;

onMount(async () => {
  ctx = canvas.getContext("2d");

  ctx.fillStyle = "green";
  ctx.fillRect(10, 10, 150, 100);
})


function redraw() {

}



</script>

<canvas bind:this={canvas} class="mycanvas" width="400" height="400"></canvas>



<style>
  .mycanvas {
    border: 1px solid black;
  }
  
  
</style>
