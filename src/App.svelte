<script>
  let search = '';

  function formSubmitted(event) {
    console.log(search);
  }
</script>

<style>
</style>

<form on:submit|preventDefault={formSubmitted}>
  <label for="search">Search</label>
  <input bind:value={search} id="search" name="search" />
  <button type="submit">Submit</button>
</form>

<h2>{search}</h2>
