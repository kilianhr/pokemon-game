<script>
import PokemonOptions from '../components/PokemonOptions.vue'
import PokemonPicture from '../components/PokemonPicture.vue'
import Pokedex from '../components/Pokedex.vue'

import getPokemonOptions from '../helpers/getPokemonOptions'

export default {
    components: { PokemonOptions, PokemonPicture, Pokedex },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: '',
            catched: []
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()
            const rndInt = Math.floor(Math.random() * 4)

            this.pokemon = this.pokemonArr[rndInt]
        },
        checkAnswer (selectedId) {
            this.showPokemon = true
            this.showAnswer= true
            if (selectedId === this.pokemon.id) {
              this.catched.push(selectedId)
              this.message = `Correcto, ${this.pokemon.name}`
            } else {
              this.message = `Oops, era ${this.pokemon.name}`
            }

        },
        newGame () {
            this.showAnswer= false
            this.showPokemon = false
            this.pokemon = null
            this.mixPokemonArray()
        }
    },
    mounted () {
        this.mixPokemonArray()
    },
}
</script>

<template>
    <div v-if="!pokemon" id="loading">
        <div class="pokeball" id="normal"></div>
        <div class="pokeball" id="great"></div>
        <div class="pokeball" id="ultra"></div>
        <div class="pokeball" id="master"></div>
        <div class="pokeball" id="safari"></div>
    </div>
    <v-content v-else class="d-flex justify-center pa-8">
      <v-row no-gutters>
          <v-col
              cols="12"
              sm="12"
          >
            <v-card>
              <v-card-item>
                  <h1 class="text-center">¿Quién es este pokémon?</h1>
              </v-card-item>
              <v-card-text>
                  <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
                  <PokemonOptions :pokemons="pokemonArr" @selection="checkAnswer" :disabledOptions="showAnswer" />
              </v-card-text>
              <v-card-actions v-if="showAnswer">
                  <v-row>
                      <v-col cols="12">
                          <h2 class="text-center">{{ message }}</h2>
                      </v-col>
                      <v-col cols="6" offset="3">
                          <v-btn
                              block
                              class="text-none mb-4"
                              color="indigo-darken-3"
                              size="x-large"
                              variant="flat"
                              @click="newGame"
                          >
                              Otra Captura
                          </v-btn>
                      </v-col>
                  </v-row>
              </v-card-actions>
          </v-card>
          </v-col>
          <v-col
            cols="12"
            sm="12"
            class="mt-4"
          >
              <Pokedex :catched="catched"/>
          </v-col>
      </v-row>
    </v-content>
</template>
