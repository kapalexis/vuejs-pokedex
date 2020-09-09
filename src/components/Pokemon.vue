<template>

        <div class="col-sm mb-4">
        <div>
   
               
                <div class="card " style="width: 18rem;">
            <img  :src='pokemonSprite' class="card-img-top" alt="">
            <div class="card-body">
                <h5 class="card-title d-flex justify-content-center"><b class="pr-2"> #{{urlPokeId}} </b> {{name | upper}}</h5>
                
            </div>
            <ul class="list-group list-group-flush">
                <li class="list-group-item">Type: {{pokemonType}} </li>
                
            </ul>
            
           
</div>
    
</div>
</div>

</template>

<script>
import axios from 'axios'

export default {
    
    created: function() {
        axios.get(this.url).then(
             res => {
                
                this.pokemonType = res.data.types[0].type.name
                this.pokemonSprite = res.data.sprites.front_default
                      
                      console.log(this.urlPokeId) 
                
    }
  )
    },
    data: function(){
        return{
            pokemonSprite: '',
            pokemonType: '',
            urlPokeId: this.url.match(/\d+/g).slice(-1).join("")
            
        }

    },
    props: {
        name: String,
        index: Number,
        url: String,
    },

    filters: {
        upper: function (value){
            let upperLetter = value[0].toUpperCase() + value.slice(1)
            return upperLetter
             
        }
    },
    
}
</script>

<style>

</style>