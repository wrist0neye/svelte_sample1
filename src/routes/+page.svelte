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
  import AudioPlayer from "../practice/Audio_/AudioPlayer.svelte";
  import {tracks} from "../practice/Audio_/tracks.js"
</script>

<div class="centered">
	{#each tracks as track}
		<AudioPlayer {...track} />
	{/each}
</div>

<style>
	.centered {
		display: flex;
		flex-direction: column;
		height: 100%;
		justify-content: center;
		gap: 0.5em;
		max-width: 40em;
		margin: 0 auto;
	}
</style>