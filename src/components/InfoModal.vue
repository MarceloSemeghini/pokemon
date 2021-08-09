<template v-if="!loading">
    <div v-if="modalOpen" class="modal_Background">
        <div class="infoModal">
            <img :src="pokemonInfo.sprites.front_default" alt="">
            <div>
                <h2>Games: {{filterGames()}}</h2>
                <h2>Encounters: {{filterEncounters()}}</h2>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name: "InfoModal",
    data(){
        return{
            encounterLocations: [],
            loading: false
        }
    },
    props: {
        pokemonInfo: Object,
        modalOpen: Boolean
    },
    async created() {
        this.loading = true
        const response = await fetch(this.pokemonInfo.location_area_encounters)
        const data = await response.json();
        this.encounterLocations = data;
        this.loading = false
    },
    methods: {
        filterEncounters(){
            var allEncounters = ""
            {if (this.encounterLocations.length != 0){
                this.encounterLocations.map(data =>
                    {if(allEncounters == ""){
                        allEncounters += data.location_area.name.split("-").join(" ")
                    }else{
                    allEncounters += ", " + data.location_area.name.split("-").join(" ")
                    }} 
                )
            }else
                return "none"
            }
            return allEncounters
        },
        filterGames(){
            var allGames = ""
            this.pokemonInfo.game_indices.map(data =>
                {if(allGames == ""){
                    allGames += data.version.name
                }else{
                   allGames += ", " + data.version.name 
                }}                
            )
            return allGames
        }
    }
}
</script>
