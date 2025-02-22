<script>
  import { onMount } from "svelte";
  import sentences from "../../lib/data/sentencesData.js";
  let textElement = [];
  let rectElement = [];
  let screenWidth;
  let screenHeight;

  const updateScreenSize = () => {
    const width = window.innerWidth;
    if (width > 1024) {
      screenWidth = "large";
      screenHeight = 300;
    } else if (width >= 768 && width <= 1024) {
      screenWidth = "medium";
      screenHeight = 400;
    } else {
      screenWidth = "small";
      screenHeight = 500;
    }
  };

  onMount(() => {
    updateScreenSize();

    textElement.forEach((element, index) => {
      const bbox = element.getBBox();
      rectElement[index].setAttribute("x", bbox.x);
      rectElement[index].setAttribute("y", bbox.y);
      rectElement[index].setAttribute("width", bbox.width);
      rectElement[index].setAttribute("height", bbox.height);
    });
  });
</script>

<div class="svg-container svg-large" style="margin: 0 auto; width: 60%;">
  <svg width="100%" height={screenHeight}>
    <rect width="100%" height="100%" fill="orange" stroke="black" />
    {#each sentences as { text, position, rotation }, index}
      <g
        transform={`rotate(${rotation}, ${position["large"].x}, ${position["large"].y})`}
      >
        <rect
          bind:this={rectElement[index]}
          id={`rect-${index}`}
          fill="none"
          stroke="black"
        />
        <text
          bind:this={textElement[index]}
          id={`text-${index}`}
          x={position["large"].x}
          y={position["large"].y}
          alignment-baseline="middle"
          text-anchor="middle"
          fill="black"
          font-size="12"
        >
          {text}
        </text>
      </g>
    {/each}
  </svg>
</div>

<div class="svg-container svg-medium" style="margin: 0 auto; width: 60%;">
  <svg width="100%" height={screenHeight}>
    <rect width="100%" height="100%" fill="none" stroke="black" />
    {#each sentences as { text, position, rotation }, index}
      <g
        transform={`rotate(${rotation}, ${position["medium"].x}, ${position["medium"].y})`}
      >
        <rect
          bind:this={rectElement[index]}
          id={`rect-${index}`}
          fill="none"
          stroke="black"
        />
        <text
          bind:this={textElement[index]}
          id={`text-${index}`}
          x={position["medium"].x}
          y={position["medium"].y}
          alignment-baseline="middle"
          text-anchor="middle"
          fill="black"
          font-size="12"
        >
          {text}
        </text>
      </g>
    {/each}
  </svg>
</div>

<div class="svg-container svg-small" style="margin: 0 auto; width: 60%;">
  <svg width="100%" height={screenHeight}>
    <rect width="100%" height="100%" fill="yellow" stroke="black" />
    {#each sentences as { text, position, rotation }, index}
      <g
        transform={`rotate(${rotation}, ${position["small"].x}, ${position["small"].y})`}
      >
        <rect
          bind:this={rectElement[index]}
          id={`rect-${index}`}
          fill="none"
          stroke="black"
        />
        <text
          bind:this={textElement[index]}
          id={`text-${index}`}
          x={position["small"].x}
          y={position["small"].y}
          alignment-baseline="middle"
          text-anchor="middle"
          fill="black"
          font-size="12"
        >
          {text}
        </text>
      </g>
    {/each}
  </svg>
</div>

<style>
  .svg-container {
    display: none;
  }

  @media (min-width: 1024px) {
    .svg-container.svg-large {
      display: block;
    }
  }

  @media (min-width: 768px) and (max-width: 1024px) {
    .svg-container.svg-medium {
      display: block;
    }
  }

  @media (max-width: 767px) {
    .svg-container.svg-small {
      display: block;
    }
  }
</style>
