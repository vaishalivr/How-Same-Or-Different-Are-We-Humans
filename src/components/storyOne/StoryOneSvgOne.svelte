<script>
  import { onMount } from "svelte";
  import sentences from "../../lib/data/sentencesData.js";

  let height = 600;
  let textElement;
  let rectElement;
  let svgContainer;
  let screenSize;
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

  const updateScreenSize = () => {
    if (window.innerWidth < 768) {
      screenSize = "small";
    } else if (window.innerWidth >= 768 && window.innerWidth <= 1024) {
      screenSize = "medium";
    } else {
      screenSize = "large";
    }
  };

  onMount(() => {
    updateScreenSize();
    window.addEventListener("resize", updateScreenSize);

    sentences.forEach((sentence, index) => {
      const rectElement = document.getElementById(`rect-${index}`);
      const textElement = document.getElementById(`text-${index}`);
      getBoundingBox(textElement, rectElement, sentence.fill);
    });

    return () => window.removeEventListener("resize", updateScreenSize);
  });

  let svgClasses = [
    { className: "svg-small", height: "600", fill: "green" },
    { className: "svg-medium", height: "500", fill: "yellow" },
    { className: "svg-large", height: "400", fill: "green" },
  ];
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
    fill: black;
    font-size: 1.5rem;
    text-anchor: middle;
  }

  .svg-container {
    display: none;
  }

  @media (min-width: 1024px) {
    .svg-large {
      display: block;
    }
  }

  @media (min-width: 768px) and (max-width: 1024px) {
    .svg-medium {
      display: block;
    }
  }

  @media (max-width: 768px) {
    .svg-small {
      display: block;
    }
  }
</style>
