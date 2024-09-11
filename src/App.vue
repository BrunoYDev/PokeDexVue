<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter has-text-centered">
      <figure class="image is-inline-block">
        <img src="./assets/logo.png" alt="Pokedex Logo" class="image is-128x128">
      </figure>  
      <h4 class="is-size-4">Pokedex VUE</h4>
      <input type="text" placeholder="Search pokemon by name" v-model="searchText" class="input is-rounded">
      <button class="button is-fullwidth" id="searchBtn" @click="searchResult">Search</button>
      <hr>
      <div v-for="poke in filteredPokemons" :key="poke.url">
      <pokecard :name="poke.name" :url="poke.url"/>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import pokecard from './components/pokecard.vue';

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      searchText: '',
      filteredPokemons: []
    }
  },
  components:{
      pokecard,
  },
  created(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  methods:{
    searchResult(){
      this.filteredPokemons = this.pokemons;
      if(this.searchText == '' || this.searchText == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.searchText);
      }
    }
  },
  computed:{
    // searchResult(){
    //   if(this.searchText == '' || this.searchText == ' '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.searchText);
    //   }
    // }
  }
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
#searchBtn{
  margin-top: 2%;
}
</style>
