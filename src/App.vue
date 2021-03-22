
<template>
  <div id="app">


    <div class="column is-one-quarter is-offset-5">
    <img src="./assets/pokedex.png" alt="">

    <hr>
    <h4 class="is-size-4">By Ronald</h4>
    <input type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded" id="inputBusca">
    <button class="button is-fullwidth is-success" id="busca-btn" @click="buscar">Buscar</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
        <!-- <h1>{{index+1}} {{poke.name}}</h1> -->
      </div>
    </div>

  </div>
</template>


<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  
  name: 'App',

  components:{
    Pokemon
  },
  
  data(){
    return{
      pokemons:[],
      filteredPokemons:[],
      busca:'',
    }
  },

  created:function(){
    // console.log(axios);
    // console.log("teste");
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res=>{
      console.log("Pegou a lista de pokemons");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
      // console.log(this.pokemons);
    }).catch(err=>{
      console.log(err);
    });
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == "" || this.busca == " "){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemons => pokemons.name == this.busca);
      }

    }
  },
  computed:{
    // resultadoBusca: function(){
    //   if(this.busca == "" || this.busca == " "){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon=> pokemon.name == this.busca)
    //   }
    // }
  }
 
}
</script>


<style>
#app{
  text-align: center;
}
#busca-btn{
  margin-top: 2%;
}
</style>
