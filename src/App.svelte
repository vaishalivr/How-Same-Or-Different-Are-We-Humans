<script>
  let currentPage = 0;

  function handleScroll() {
    currentPage += 1;
    const mainContainer = document.querySelector(".main-container");
    mainContainer.style.transform = `translateX(-${currentPage * 100}vw)`;
  }

  function handleScrollBack() {
    if (currentPage > 0) {
      currentPage -= 1;
      updateTransform();
    }
  }

  function updateTransform() {
    const mainContainer = document.querySelector(".main-container");
    mainContainer.style.transform = `translateX(-${currentPage * 100}vw)`;
  }
</script>

<main>
  <div class="main-container">
    <div class="story-one">
      <button on:click={handleScroll}>Button</button>
    </div>
    <div class="story-two">
      <button on:click={handleScrollBack}>Go Back</button>
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
  .story-one {
    width: 50%;
    border: 1px solid red;
  }
  .story-two {
    width: 50%;
    border: 1px solid green;
  }
</style>
