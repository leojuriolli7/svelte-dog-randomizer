<script lang="ts">
  import { onMount } from "svelte";
  import Button from "./lib/components/Button.svelte";

  type Response = {
    message: string;
  };

  const API_ENDPOINT = "https://dog.ceo/api/breeds/image/random";

  let isFetching = false;
  let image: string;

  function fetchDog() {
    isFetching = true;

    fetch(API_ENDPOINT)
      .then(async (res) => {
        const response: Response = await res.json();

        image = response.message;
      })
      .finally(() => {
        isFetching = false;
      });
  }

  onMount(() => {
    fetchDog();
  });
</script>

<main>
  <div class="title">
    <img src="svelte.svg" alt="Svelte logo" />
    <h1>Dog Randomizer</h1>
  </div>
  <Button variant="brand" on:click={fetchDog} loading={isFetching}>
    Randomize dog
  </Button>

  <img class="dog-image" src={image} alt="Random dog" />
</main>

<style lang="scss">
  main {
    display: flex;
    flex-direction: column;
    height: 100vh;
    align-items: center;
  }

  .title {
    display: flex;
    align-items: center;
    gap: 6px;
    margin-top: 5rem;
    margin-bottom: 2rem;
  }

  .dog-image {
    border-radius: 10px;
    height: 400px;
    margin-top: 1rem;
    object-fit: cover;
    width: 400px;
    margin-top: 2rem;

    @media (max-width: 440px) {
      aspect-ratio: 1;
      height: auto;
      width: 90%;
    }
  }
</style>
