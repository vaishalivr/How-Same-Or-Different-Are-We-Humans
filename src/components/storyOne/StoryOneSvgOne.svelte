<script>
  import { onMount } from "svelte";
  import sentences from "../../lib/data/sentencesData.js";

  let height = 600;
  let textElement;
  let rectElement;
  let bbPadding = 8;

  function getBoundingBox(textElement, rectElement, fillRatio) {
    if (textElement && rectElement) {
      const bbox = textElement.getBBox();
      rectElement.setAttribute("x", bbox.x - bbPadding / 2);
      rectElement.setAttribute("y", bbox.y - bbPadding / 2);
      rectElement.setAttribute("width", fillRatio * (bbox.width + bbPadding));
      rectElement.setAttribute("height", bbox.height + bbPadding);
    }
  }

  onMount(() => {
    sentences.forEach((sentence, index) => {
      const rectElement = document.getElementById(`rect-${index}`);
      const textElement = document.getElementById(`text-${index}`);
      getBoundingBox(textElement, rectElement, sentence.fill);
    });
  });
</script>

<div style="width: 60%; margin:0 auto">
  <svg width="100%" {height}>
    <rect width="100%" {height} stroke="black" stroke-width="2" fill="none" />

    {#each sentences as { text, x, y, rotation }, index}
      <g transform={`rotate(${rotation} ${x} ${y})`}>
        <rect bind:this={rectElement} id="rect-{index}" fill="yellow"></rect>
        <text
          bind:this={textElement}
          id="text-{index}"
          {x}
          {y}
          alignment-baseline="middle"
          text-anchor="middle"
          font-size="0.6rem"
          fill="black"
        >
          {text}
        </text>
      </g>
    {/each}
  </svg>
</div>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Caveat:wght@600&display=swap");
  text {
    font-family: "Caveat", cursive;
    font-size: 30px;
    fill: black;
  }
</style>
