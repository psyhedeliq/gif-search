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
  <label for="search">Search</label>
  <input bind:value={search} id="search" name="search" />
  <button type="submit">Submit</button>
</form>

{#if loading}
  <img
    src="https://media.giphy.com/media/3y0oCOkdKKRi0/giphy.gif"
    alt="Elmer Runnig Circles" />
{/if}

<div class="results">
  {#each gifs as gif}<img src={gif} alt="GIF" />{/each}
</div>
