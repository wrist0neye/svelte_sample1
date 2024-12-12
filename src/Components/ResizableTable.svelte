<script>
  // 다음에는 formula parser를 만들어볼 예정.
  import { onMount } from 'svelte';

  let table;
  let isResizingCol = false;
  let isResizingRow = false;
  let startX, startY, startWidth, startHeight;
  let currentCol, currentRow;
  let currentPosition = {x : 0, y: 0};
  let isDragging = false;
  let offset = {x: 0, y : 0};

  function onMouseDownCol(event, col) {
    isResizingCol = true;
    startX = event.clientX;
    currentCol = col;
    startWidth = currentCol.offsetWidth;
    document.addEventListener('mousemove', onMouseMoveCol);
    document.addEventListener('mouseup', onMouseUpCol);
  }

  function onMouseMoveCol(event) {
    if (!isResizingCol) return;
    const dx = event.clientX - startX;
    currentCol.style.width = `${startWidth + dx}px`;
  }

  function onMouseUpCol() {
    isResizingCol = false;
    document.removeEventListener('mousemove', onMouseMoveCol);
    document.removeEventListener('mouseup', onMouseUpCol);
  }

  function onMouseDownRow(event, row) {
    isResizingRow = true;
    startY = event.clientY;
    currentRow = row;
    startHeight = currentRow.offsetHeight;
    document.addEventListener('mousemove', onMouseMoveRow);
    document.addEventListener('mouseup', onMouseUpRow);
  }

  function onMouseMoveRow(event) {
    if (!isResizingRow) return;
    const dy = event.clientY - startY;
    currentRow.style.height = `${startHeight + dy}px`;
  }

  function onMouseUpRow() {
    isResizingRow = false;
    document.removeEventListener('mousemove', onMouseMoveRow);
    document.removeEventListener('mouseup', onMouseUpRow);
  }

  onMount(() => {
    const colSeps = document.querySelectorAll('.col_sep');
    colSeps.forEach(colSep => {
      colSep.addEventListener('mousedown', (event) => onMouseDownCol(event, colSep.parentElement));
    });

    const rowSeps = document.querySelectorAll('.row_sep');
    rowSeps.forEach(rowSep => {
      rowSep.addEventListener('mousedown', (event) => onMouseDownRow(event, rowSep.parentElement));
    });
  });

  function dragMouseDown(event) {
    event.preventDefault();
    isDragging = true;
    offset.x = event.clientX - currentPosition.x;
    offset.y = event.clientY - currentPosition.y;
    // document.addEventListener('mousemove', elementDrag);
    // document.addEventListener('mouseup', closeDragElement);
  }

  function dragMouseMove(event) {
    if (isDragging) {
      currentPosition.x = event.clientX - offset.x;
      currentPosition.y = event.clientY - offset.y;
      // table.style.left = currentPosition.x + 'px';
      // table.style.top = currentPosition.y + 'px';
    }
  }

  function dragMouseUp(event) {
    isDragging = false;
    // document.removeEventListener('mousemove', elementDrag);
    // document.removeEventListener('mouseup', closeDragElement);
  }
</script>

<style>
  table {
    border-collapse: collapse;
    width: 100%;
    margin : 2px;
  }
  th, td {
    border: 1px solid black;
    padding: 8px;
    text-align: left;
    position: relative;
  }
  .col_sep {
    position: absolute;
    right: -1px;
    top: 0;
    bottom: 0;
    width: 2px;
    cursor: col-resize;
    background-color: transparent;
    transition: ease-in-out 0.1s;
  }
  .col_sep:hover{
    background-color: #666;
    border: 1px solid #666;
  }
  .col_sep:active{
    background-color: #666;
    border: 1px solid #666
  }
  .row_sep {
    position: absolute;
    bottom: -1px;
    left: 0;
    right: 0;
    height: 2px;
    cursor: row-resize;
    background-color: transparent;
    transition: ease-in-out 0.1s;
  }
  .row_sep:hover{
    background-color: #666;
    border: 1px solid #666;
  }
  .row_sep:active{
    background-color: #666;
    border: 1px solid #666
  }

  .table_container {
    overflow-x: auto;
    /* transition: all 0.2s ease-in-out; */
  }
  .table_menu {
    display: flex;
    justify-content: space-between;
    padding: 8px;
    background-color: #f1f1f1;
    border-bottom: 1px solid #ccc;
  }
  .table_menu:hover{
    cursor: move;
    background-color: yellow;
  }
  .table_widget{
    position: absolute;
    display: flex;
    flex-direction: column;
    gap: 8px;
    max-width: 600px;
    max-height: 400px;
    padding: 2px;
    border: 1px dashed blue;
  }
  .table_widget:hover{
    border : 2px solid #ccc;
    border-radius: 5px;
    transform: translateX(-1px) translateY(-1px);
  }
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
  <div class="table_widget"
    style="left: {currentPosition.x}px; top: {currentPosition.y}px;"
    on:mousemove={dragMouseMove}
    on:mouseup={dragMouseUp}>
    <div
      class="table_menu"
      on:mousedown={dragMouseDown}></div>
    <div class="table_container">
      <table bind:this={table}>
        <thead>
          <tr>
            <th>
              Header 1
              <div class="col_sep"></div>
              <div class="row_sep"></div>
            </th>
            <th>
              Header 2
              <div class="col_sep"></div>
            </th>
            <th>
              Header 3
              <div class="col_sep"></div>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>
              Data 1
              <div class="row_sep"></div>
            </td>
            <td>
              Data 2
            </td>
            <td>
              Data 3
            </td>
          </tr>
          <tr>
            <td>
              Data 4
              <div class="row_sep"></div>
            </td>
            <td>
              Data 5
            </td>
            <td>
              Data 6
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
