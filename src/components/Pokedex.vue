<script>
import PokemonPicture from '../components/PokemonPicture.vue'

export default {
    name: 'Pokedex',
    components: { PokemonPicture },
    data() {
        return {
            pokemons: []
        }
    },
    props: {
        catched: {
            type: Array,
            required: true
        }
    },
    mounted () {
        this.getAllPokemons()
    },
    methods: {
        getAllPokemons() {
            const pokemonsArr = Array.from( Array(151) )
            this.pokemons = pokemonsArr.map((_, index) => index + 1)
        }
    },
}
</script>

<template>
    <div>
        <v-card>
              <v-card-item>
                <h1 class="text-center">Pokemons Capturados</h1>
              </v-card-item>
              <v-card-text>
                <div class="pokemon-grid">
                    <div v-for="pokemon in pokemons" :key="pokemon" >
                        <PokemonPicture :pokemonId="pokemon" :showPokemon="catched.includes(pokemon)" pokedex />
                    </div>
                </div>
              </v-card-text>
        </v-card>
    </div>
</template>

<style lang="scss" scoped>
.pokemon-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    overflow: scroll;
    overflow-x: hidden;
    height: 600px;
}
</style>
