<!-- <script>
  import ResizableTable from "../Components/ResizableTable.svelte";
</script>

<style>
  .sketch_book {
    position: relative;
    width: 100%;
    height: 100vh;
    background-color: #f1f1f1;
    border-radius: 5px;
    padding: 8px;
  }
</style>


<div class="sketch_book">
  <ResizableTable></ResizableTable>
  <ResizableTable></ResizableTable>
</div> -->

<!-- 위 코드는 메인으로 사용할 코드 -->

<script>
  import {paint} from '../practice/this binding/gradient.js';

  let canvas;

  $effect(()=> {
    const context = canvas.getContext('2d');

    let frame = requestAnimationFrame(function loop(t) {
      frame = requestAnimationFrame(loop);
      paint(context, t);
    });

    return () => {
      cancelAnimationFrame(frame);
    };
  });
</script>

<canvas bind:this={canvas} width = {32} height={32}></canvas>

<style>
  canvas {
    position : fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #666;
    mask: url('../practice/this binding/svelte-logo-mask.svg') 50% 50% no-repeat;
    maks-size: 60vmin;
    -webkit-mask: url('../practice/this binding/svelte-logo-mask.svg') 50% 50% no-repeat;
    -webkit-mask-size: 60vmin;
  }
</style>