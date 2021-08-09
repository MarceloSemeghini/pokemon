<template>
    <div v-if="!loading" class="PokemonChart" @click="onClick()" :style="`background-color:#${filterType()}`">
        <img :src="pokemonInfo.sprites.front_default" alt="">
        <h1>{{pokemon.name}}</h1>
        <InfoModal :pokemonInfo="pokemonInfo" :modalOpen="modalOpen"/>
    </div>
</template>

<script>
import InfoModal from './InfoModal.vue'
export default{
    name: "Pokemon",
    data(){
        return{
            pokemonInfo: {},
            modalOpen: false,
            loading: false
        }
    },
    props: {
        pokemon: Object,
        text: String
    },

    async created() {
        this.loading = true
        const response = await fetch(this.pokemon.url)
        const data = await response.json();
        this.pokemonInfo = data;
        this.loading = false
    },
    components: {
        InfoModal
    },
    methods:{
        filterType(){
            {switch (this.pokemonInfo.types[0].type.name){
                case "normal":
                    return "a0a29f"
                case "grass":
                    return "6abd5a"
                case "fire":
                    return "f1a34c"
                case "water":
                    return "459fdf"
                case "bug":
                    return "9bbb31"
                case "flying":
                    return "98bcec"
                case "poison":
                    return "b066cf"
                case "dragon":
                    return "276dc7"
                case "ghost":
                    return "4e6fbc"
                case "psychic":
                    return "ed817f"
                case "electric":
                    return "f9d850"
                case "rock":
                    return "cebb8b"
                case "fairy":
                    return "eb93e5"
                case "ground":
                    return "de7c4d"
                case "steel":
                    return "4f95a3"
                case "fighting":
                    return "d64b5f"
                case "ice":
                    return "73d0c2"
                case "dark":
                    return "73d0c2"
            }}
        },
        onClick(){
            this.modalOpen = !this.modalOpen
        }
    }
}
</script>
