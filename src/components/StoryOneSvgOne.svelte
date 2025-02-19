<script>
  import { onMount } from "svelte";
  let height = 600;
  let stroke = "black";
  let strokeWidth = "2";
  let fill = "none";
  let textElement;
  let rectElement;
  let bbPadding = 15;

  function getBoundingBox() {
    if (textElement && rectElement) {
      const bbox = textElement.getBBox();
      rectElement.setAttribute("x", bbox.x - bbPadding / 2);
      rectElement.setAttribute("y", bbox.y - bbPadding / 2);
      rectElement.setAttribute("width", bbox.width + bbPadding);
      rectElement.setAttribute("height", bbox.height + bbPadding);
    }
  }
  onMount(() => {
    getBoundingBox();
  });
</script>

<div style="width: 60%; margin:0 auto">
  <svg width="100%" {height}>
    <rect width="100%" {height} {stroke} stroke-width={strokeWidth} {fill} />
    <g transform={`rotate(-30)`}>
      <rect bind:this={rectElement} fill="yellow"></rect>
      <text
        bind:this={textElement}
        x="10%"
        y="20%"
        alignment-baseline="middle"
        text-anchor="middle"
        font-size="1rem"
        fill="black"
      >
        night sky at 4pm
      </text>
    </g>
  </svg>
</div>
