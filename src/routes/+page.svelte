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
  import Keypad from "../practice/Keypad.svelte";

  let pin = $state('');

  let view = $derived(pin ? pin.replace(/\d(?!$)/g, '•') : 'enter your pin');

  function onsubmit(){
    alert(`submitted ${pin}`);
  }
</script>

<h1 style="opacity: {pin ? 1 : 0.4}">
  {view}
</h1>

<Keypad bind:value={pin} {onsubmit}/>