<script>
  import titleDrawingsData from "../lib/data/titleDrawingsData.js";
  const { houseData } = titleDrawingsData;

  function createPath(stroke) {
    const [xPoints, yPoints] = stroke;
    const pathString = xPoints
      .map((x, i) => `${i === 0 ? "M" : "L"} ${x},${yPoints[i]}`)
      .join(" ");
    console.log(pathString);
    return pathString;
  }
</script>

<div class="title">
  <svg width="100%" height="100%">
    <text x="50%" y="40%" text-anchor="middle">
      <tspan x="50%" dy="0em">How</tspan>
      <tspan x="50%" dy="1.2em">Same or Different</tspan>
      <tspan x="50%" dy="1.2em">Are We</tspan>
      <tspan x="50%" dy="3em">By Vaishali Verma</tspan>
    </text>

    <g fill="none" stroke="black" stroke-width="2" transform="scale(0.5)">
      {#each houseData as stroke}
        <path d={createPath(stroke)} />
      {/each}
    </g>
  </svg>
</div>

<style>
  .title {
    height: 100vh;
  }
  svg text {
    font-size: 2vw;
  }
</style>
