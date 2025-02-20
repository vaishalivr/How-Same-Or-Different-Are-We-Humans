<script>
  let sentences = [
    { text: "night sky past 4pm", x: 150, y: 150, rotation: -20, fill: 0.45 },
    {
      text: "seeing snow on some mornings",
      x: 800,
      y: 100,
      rotation: 25,
      fill: 0.6,
    },
    {
      text: "woodern floored bathrooms",
      x: 600,
      y: 150,
      rotation: 10,
      fill: 0.75,
    },
    {
      text: "freezing despite the sun shining",
      x: 350,
      y: 250,
      rotation: 20,
      fill: 1,
    },
    {
      text: "clothes dryer in every house",
      x: 200,
      y: 360,
      rotation: -20,
      fill: 1,
    },
    {
      text: "different units of measurements",
      x: 300,
      y: 500,
      rotation: -20,
      fill: 1,
    },
    {
      text: "drinking water directly from kitchen tap",
      x: 300,
      y: 500,
      rotation: -20,
      fill: 1,
    },
    {
      text: "kids playing indoor after school",
      x: 800,
      y: 300,
      rotation: 20,
      fill: 1,
    },
    {
      text: "Boston Celtics, Boston Bruins, New England Patriots",
      x: 600,
      y: 520,
      rotation: -10,
      fill: 1,
    },
  ];

  import { onMount } from "svelte";

  let height = 600;
  let textElement;
  let rectElement;
  let bbPadding = 15;

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
    <defs>
      <mask id="fillMask"></mask>
    </defs>
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
