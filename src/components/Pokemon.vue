<template>
    <div id="pokemon">
      <!-- <h1>{{num}} {{name | upper}}</h1>
      <small>{{url}}</small>
      <img :src=this.pokemon.front alt="">      
      <img :src=this.pokemon.back alt="">       -->
    <div class="card">
    <div class="card-image">
        <img :src=currentImg alt="Placeholder image">
    </div>
    <div class="card-content">
        <div class="media">
        
        <div class="media-content">
            <p class="title is-4">{{num}} {{name | upper}}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
        </div>
        </div>

        <div class="content">
            <button class="button is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
        </div>
    </div>
    </div>
    </div>
  
</template>

<script>
import axios from "axios";
export default {
    data(){
      return {
        isFront:true,
        currentImg: "",
        pokemon:{
            type:"",
            front:"",
            back:"",
        }
      }
    },
    created:function(){
        axios.get(this.url).then(res=>{
            // console.log(res.data.sprites.front_default);
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        });
    },
    props:{
        num:Number,
        name:String,
        url:String,
    },
    filters:{
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods:{
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
#pokemon{
    margin: 2% 0 0 0;
}

</style>