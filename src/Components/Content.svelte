<script>
  import SearchBar from './SearchBar.svelte'
  import Card from './Card.svelte'
  import { onMount } from 'svelte'
  import {v4 as uuidv4} from 'uuid'

  let allPokemon = [];
  let finalArray = [];

  //const fetch = require("node-fetch");

  /* we retrieve all basic pokemons
  this request give us an url to make another
  request to have more statistics (including image and fr name)*/
  onMount(async () => {
    const fetchPokemonBase = () => {
      fetch('https://pokeapi.co/api/v2/pokemon/?limit=151')
      .then(response => response.json())
      .then(function(allPoke) {
        // console.log(allPoke);
        allPoke.results.forEach(function(pokemon){
          // function called for each pokemon in the array
          fetchPokemonComplete(pokemon);
        })
      })
    }
    fetchPokemonBase();

    // we create an oject with name and url
    const fetchPokemonComplete = (pokemon) => {
      let objPokemonFull = {}; // object with name in fr and url
      let url = pokemon.url;
      let nameP = pokemon.name;

      fetch(url)
        .then(response => response.json())
        .then(function(pokeData){
          objPokemonFull.pic = pokeData.sprites.back_default; // images
          // console.log(pokeData);
          // we make a request by pokemon species to retrieve some other data (fr name)
          fetch(`https://pokeapi.co/api/v2/pokemon-species/${nameP}`)
          .then(reponse =>  reponse.json())
          .then(function(pokeData){
              // console.log(pokeData);
              objPokemonFull.name = pokeData.names[4].name; // french name
              allPokemon.push(objPokemonFull); // push in the array
          })
          .then(() => {
              // console.log(allPokemon);
              finalArray = allPokemon.slice(0,20) // array with only 20 pokemons
              allPokemon = allPokemon; // update var
          })
        })
    }
  });

  const goSearch = (event) => {
    console.log(event.detail.txt);

    let contentSearch = event.detail.txt;

    /* excludes all except the pokemon searched*/
    //allPokemon = allPokemon.filter(el => el.name.includes(contentSearch))
    finalArray = allPokemon.filter(el => el.name.includes(contentSearch))
  }

</script>

<SearchBar on:search-poke={goSearch} />
<div class="content">
<!-- List -->
{#each finalArray as pokemon (uuidv4())}
  <Card name={pokemon.name} pic={pokemon.pic} />
{/each}
<!-- {#each allPokemon as pokemon (uuidv4())}
  <Card name={pokemon.name} pic={pokemon.pic} />
{/each} -->
</div>

<style>

.content{
  /* if enough space */
  max-width: 1400px;
  /* else */
  width: 95%;
  padding: 0 50px;
  margin: 0 auto;
  /* align side by side */
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  /* background: orange; */
}

</style>