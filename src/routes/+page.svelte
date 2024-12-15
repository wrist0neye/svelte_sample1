<!-- <script>
  import Dragnode from "../Components/dragnode.svelte";
</script>


<div class="playground">
  <Dragnode></Dragnode>
</div>

<style>
  .playground{
    width: 100%;
    height: 800px;
    border: 2px dashed grey;
    border-radius: 10px;
    background-color: lightgray;
  }
</style> -->

<script>
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
</div>