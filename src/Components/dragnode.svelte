<script>
  let circlePosition = { x: 100, y: 100 }; // 초기 동그라미 위치
  let isDragging = false; // 드래그 상태 확인용
  let offset = { x: 0, y: 0 }; // 드래그 시작 시 마우스와 동그라미 중심의 거리

  // 드래그 시작
  function handleMouseDown(event) {
    isDragging = true;
    offset.x = event.clientX - circlePosition.x;
    offset.y = event.clientY - circlePosition.y;
  }

  // 드래그 중
  function handleMouseMove(event) {
    if (isDragging) {
      circlePosition.x = event.clientX - offset.x;
      circlePosition.y = event.clientY - offset.y;
    }
  }

  // 드래그 끝
  function handleMouseUp() {
    isDragging = false;
  }
</script>

<style>
  .container {
    width: 100%;
    height: 100vh;
    background-color: #f9f9f9;
    position: relative;
    overflow: hidden;
  }

  .circle {
    width: 50px;
    height: 50px;
    background-color: #4caf50;
    border-radius: 50%;
    position: absolute;
    cursor: grab;
  }
</style>

<div
  class="container"
  on:mousemove={handleMouseMove}
  on:mouseup={handleMouseUp}
>
  <div
    class="circle"
    style="left: {circlePosition.x}px; top: {circlePosition.y}px"
    on:mousedown={handleMouseDown}
  ></div>
</div>