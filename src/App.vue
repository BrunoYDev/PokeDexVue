<template>
  <div id="app">
    <div v-for="(poke,index) in pokemons" :key="index">
      <pokecard :name="poke.name" :url="poke.url" :num="index+1"/>
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
      pokemons: []
    }
  },
  components:{
      pokecard,
  },
  created(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results;
    })
  }
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
