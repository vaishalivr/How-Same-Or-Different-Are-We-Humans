<script>
  import StoryOneTitle from "./components/StoryOneTitle.svelte";
  import StoryTwoTitle from "./components/StoryTwoTitle.svelte";
  import StoryOneText from "./components/StoryOneText.svelte";
  import StoryTwoText from "./components/StoryTwoText.svelte";

  let currentPage = 0;

  function handleScroll() {
    currentPage += 1;
    const mainContainer = document.querySelector(".main-container");
    mainContainer.style.transform = `translateX(-${currentPage * 100}vw)`;
  }

  function handleScrollBack() {
    if (currentPage > 0) {
      currentPage -= 1;
      const mainContainer = document.querySelector(".main-container");
      mainContainer.style.transform = `translateX(-${currentPage * 100}vw)`;
    }
  }
</script>

<main>
  <div class="main-container">
    <div class="story-one">
      <div class="main-story-one">
        <StoryOneTitle />
        <StoryOneText />
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
</main>

<style>
  .main-container {
    display: flex;
    width: 200vw;
    height: 100vh;
    overflow-x: hidden;
    transform: translateX(0);
    transition: transform 0.5s ease;
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
