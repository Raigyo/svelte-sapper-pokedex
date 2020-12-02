<script>
  import {createEventDispatcher} from 'svelte';

  const dispatch = createEventDispatcher(); // custom event

  let search = '';
  const searchFunc = () => {
    dispatch('search-poke', {txt: search}) // event listener
    search = "";
  }
</script>

<form class="form-search" on:submit|preventDefault={searchFunc}>
  <label for="search">Search a Pokémon</label>
  <input bind:value={search} type="text" id="researchcherche" placeholder="Search a Pokémon">
  <button type="submit">Search</button>
</form>

<style>
    .form-search {
        margin: 200px auto 50px auto;
        max-width: 1100px;
        width: 100%;
        padding: 0 50px;
        /* background: crimson; */
        display: flex;
        align-content: center;
        flex-direction: column;
    }
    .form-search input, .form-search label  {
        max-width: 1100px;
        width: 100%;
    }
    .form-search label {
        font-size: 25px;
        border: none;
        padding: 10px 0px;
    }
    .form-search input {
        font-size: 20px;
        padding: 20px;
        background: rgb(240,197,240);
    }
</style>