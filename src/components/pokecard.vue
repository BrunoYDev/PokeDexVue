<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="currentImg"
            alt="Pokemon Image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content">
          <hr>
          <button @click="changeSprite">Change Sprite</button>
          <hr>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    name: String,
    url: String,
  },
  computed: {
    upper() {
      let newName = this.name[0].toUpperCase() + this.name.slice(1);
      return newName;
    },
  },
  created() {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: '',   
      pokemon: {},
    };
  },
  methods:{
    changeSprite(){

        if(this.isFront){
            this.isFront = false;
            this.currentImg = this.pokemon.back;
        }else{
            this.isFront = true;
            this.currentImg = this.pokemon.front;
        }
    }
  }
};
</script>
    
<style>
    #pokemon{
        margin-top: 2%;
    }
</style>