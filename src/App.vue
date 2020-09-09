<template>

 
    <div class = "bg-light">

      <h1 class="d-flex justify-content-center pt-2 pb-3">Vue Pokedex</h1>

          <form class="form-inline justify-content-center pt-2 pb-3">
          <input class="form-control form-control-lg" type="text" placeholder="Find Pokemon" v-model="busca">
          </form>

      <div class= "row d-flex justify-content-center pb-5 mt-3">
    

          <div v-for="(name, index ) in resultadoBusca" :key="name.url"> 
          <Pokemon :name="name.name" :index="index+1" :url="name.url" />


            
          </div>
        </div>
      </div>
   
    
  
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',  
  data(){
    return {
      pokemons: [],
      busca: ''
    }
  },
  created: function(){ //call it when created (useEffect?)
  axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(
    res => {
      
      this.pokemons= res.data.results
      console.log(this.pokemons)
    }
  )
    },
  components:{
    Pokemon
  },

  computed:{
    resultadoBusca: function(){
      let busca = this.busca.toLowerCase()
      
      if (busca == '' || busca == ' '){
        return this.pokemons
      }
      else{
        return this.pokemons.filter(poke => poke.name.includes(busca))
        
      }
    }
  }
}
</script>

<style>
</style>
