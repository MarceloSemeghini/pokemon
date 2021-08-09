<template>
    <Pokemon v-for="pokemon in pokemons" :key="pokemon.name" :pokemon="pokemon"/>

    <button v-if="offset > 0" @click="previousPage" class="left"> 
        <img src="http://cdn.onlinewebfonts.com/svg/img_266597.png" alt="right">  
    </button>
    <button @click="nextPage" class="right"> 
        <img src="http://cdn.onlinewebfonts.com/svg/img_266597.png" alt="right">    
    </button>
</template>

<script>
import Pokemon from './Pokemon.vue'

export default{
    name: "Pokemons",
    data() {
        return{
            offset: 0,
            pokemons: []
        }
    },
    mounted() {
        this.loadPokemons()
    },
    components: {
        Pokemon
    },
    methods: {
        async loadPokemons(){
            await fetch(`https://pokeapi.co/api/v2/pokemon?limit=20&offset=${this.offset}`)
             .then(res => res.json())
             .then(data => this.pokemons = data.results)
             .catch(error => console.log(error.message))
        },
        previousPage(){
            this.offset -= 20
            this.loadPokemons()
        },
        nextPage(){
            this.offset += 20
            this.loadPokemons()
        }
    },
}
</script>
