<script>
  import titleDrawingsData from "../../lib/data/titleDrawingsData.js";
  let baseDrawings = Object.values(titleDrawingsData);
  let requiredDrawings = 84;
  let drawings = Array.from(
    { length: requiredDrawings },
    (_, i) => baseDrawings[i % baseDrawings.length]
  );

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

  function createPath(stroke) {
    const [xPoints, yPoints] = stroke;
    return xPoints
      .map((x, i) => `${i === 0 ? "M" : "L"} ${x},${yPoints[i]}`)
      .join(" ");
  }
</script>

<div class="title-container">
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

    <g fill="none" stroke="black" stroke-width="2">
      {#each drawings as drawing, index}
        {#if index < titleGrid.numCols * titleGrid.numRows}
          <g
            transform="translate({(index % titleGrid.numCols) *
              titleGrid.spacing +
              titleGrid.spacing / 8}, 
              {Math.floor(index / titleGrid.numCols) * titleGrid.spacing +
              titleGrid.spacing / 8}) 
        scale(0.3)"
          >
            {#each drawing as stroke}
              <path d={createPath(stroke)} />
            {/each}
          </g>{/if}
      {/each}
    </g>
  </svg>
</div>

<style>
  .title-container {
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
