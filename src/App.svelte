<script>
  import StoryOneTitle from "./components/storyOne/StoryOneTitle.svelte";
  import StoryTwoTitle from "./components/storyTwo/StoryTwoTitle.svelte";
  import StoryOneText from "./components/storyOne/StoryOneText.svelte";
  import StoryTwoText from "./components/storyTwo/StoryTwoText.svelte";
  import StoryOneSvgOne from "./components/storyOne/StoryOneSvgOne.svelte";

  let currentPage = 0;

  function handleScroll() {
    currentPage += 1;
  }

  function handleScrollBack() {
    if (currentPage > 0) {
      currentPage -= 1;
    }
  }
</script>

<div class="main-container" class:scrolled={currentPage === 1}>
  <div class="story-one">
    <div class="main-story-one">
      <StoryOneTitle />
      <StoryOneText />
      <StoryOneSvgOne />
    </div>
    <div class="button-of-story-one">
      <button
        on:click={handleScroll}
        class="unstyled-button"
        id="unstyled-button-one"
        >Read AI's Story
      </button>
    </div>
  </div>

  <div class="story-two">
    <div class="button-of-story-two">
      <button
        on:click={handleScrollBack}
        class="unstyled-button"
        id="unstyled-button-two"
      >
        Go Back to Mine</button
      >
    </div>
    <div class="main-story-two">
      <StoryTwoTitle />
      <StoryTwoText />
    </div>
  </div>
</div>

<style>
  .main-container {
    display: flex;
    width: 200vw;
    height: 100vh;
    overflow-x: hidden;
    transform: translateX(0);
    transition: transform 0.5s ease;
  }
  .main-container.scrolled {
    transform: translateX(-100vw);
  }
  .story-one,
  .story-two {
    width: 50%;
    display: flex;
  }
  .main-story-one,
  .main-story-two {
    width: 90%;
    overflow-y: auto;
  }
  .button-of-story-one,
  .button-of-story-two {
    flex: 1;
    /* position: fixed; */
    height: 100vh;
    right: 0;
    top: 0;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: black;
  }
  .unstyled-button {
    all: unset;
    cursor: pointer;
    border: 1px solid black;
    color: white;
    background-color: black;
    padding: 1rem;
  }
  #unstyled-button-one {
    margin-left: -16rem;
  }
  #unstyled-button-two {
    margin-left: 12rem;
    position: absolute;
  }
  @media (max-width: 768px) {
    .unstyled-button {
      padding: 0.25rem;
    }
    #unstyled-button-one {
      margin-left: -3rem;
      font-size: 0.75rem;
    }
  }
</style>
