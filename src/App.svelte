<script>
  let search = '';
  let loading = false;
  let API_URL =
    'https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=';

  let gifs = [];

  async function formSubmitted(event) {
    loading = true;
    gifs = [];
    const url = `${API_URL}${search}`;
    const response = await fetch(url);
    const json = await response.json();
    gifs = json.data.map((gif) => gif.images.fixed_height.url);
    loading = false;
  }
</script>

<style>
  .results {
    column-count: 3;
  }

  img {
    width: 100%;
    height: auto;
  }
</style>

<form on:submit|preventDefault={formSubmitted}>
  <label style="margin-bottom:1em;" for="search">Search for your favorite GIF's!</label>
  <input bind:value={search} id="search" name="search" />
  <button type="submit">Submit</button>
</form>

{#if loading}
  <img
    src="https://media.giphy.com/media/3AMRa6DRUhMli/giphy.gif"
    alt="Loading" />
{/if}

<div class="results">
  {#each gifs as gif}<img src={gif} alt="GIF" />{/each}
</div>
