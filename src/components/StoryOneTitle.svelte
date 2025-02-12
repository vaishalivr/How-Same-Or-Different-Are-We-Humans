<script>
  import titleDrawingsData from "../lib/data/titleDrawingsData.js";
  const drawings = Object.values(titleDrawingsData);

  let screenWidth = window.innerWidth;
  let numColumns = screenWidth > 768 ? 12 : 5;
  let numRows = screenWidth > 768 ? 7 : 12;
  let spacing = 100;
  let titleGrid = {
    spacing: spacing,
    numRows: numRows,
    numCols: numColumns,
    svgWidth: numColumns * spacing,
    svgHeight: numRows * spacing,
    rectHighlightStrokeWidth: 3,
  };
</script>

<div class="title">
  <svg
    width="100%"
    height="100%"
    viewBox="0 0 {titleGrid.svgWidth} {titleGrid.svgHeight}"
  >
    <g fill="none" stroke="lightgray" stroke-width="1">
      {#each Array(titleGrid.numRows) as _, row}
        {#each Array(titleGrid.numCols) as _, col}
          <rect
            x={col * titleGrid.spacing + titleGrid.rectHighlightStrokeWidth / 2}
            y={row * titleGrid.spacing + titleGrid.rectHighlightStrokeWidth / 2}
            width={titleGrid.spacing - titleGrid.rectHighlightStrokeWidth}
            height={titleGrid.spacing - titleGrid.rectHighlightStrokeWidth}
            class="grid-cell"
          />
        {/each}
      {/each}
    </g>
  </svg>

  <p>How Same or Different Are We</p>
</div>

<style>
  .title {
    height: 100vh;
  }

  .grid-cell {
    fill: white;
    stroke-width: 0.9;
    stroke: yellowgreen;
    transition: fill 0.5s ease-in-out;
  }

  .grid-cell:hover {
    stroke-width: 3;
  }
</style>
