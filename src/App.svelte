<script>
  let search = '';
  let loading = false;
  let API_URL =
    'https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=';

  let gifs = [];

  async function formSubmitted(event) {
    loading = true;
    const url = `${API_URL}${search}`;
    const response = await fetch(url);
    const json = await response.json();
    gifs = json.data.map((gif) => gif.images.fixed_height.url);
    console.log(gifs);
  }
</script>

<style>
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
