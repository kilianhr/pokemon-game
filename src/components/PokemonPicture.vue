<script>
export default {
    name: 'PokemonPicture',
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    },
    props: {
        pokemonId: {
            type: Number,
            required: true
        },
        showPokemon: {
            type: Boolean,
            required: true,
            default: false
        },
        pokedex: {
            type: Boolean,
            default: false
        }
    }
}
</script>

<template>
    <div :class="pokedex ? 'pokedex-container' : 'pokemon-container'">
        <img :src="imgSrc" :class="!showPokemon ? 'hidden-pokemon' : 'fade-in'" alt="pokemon">
    </div>
</template>

<style lang="scss" scoped>
.pokedex-container {
  margin: 0 auto;
  position: relative;
  > img {
    height: 100px;
    transform: translate(30%, 0%);
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
  } 
}
.pokemon-container {
  height: 200px;
  width: 260px;
  margin: 0 auto;
  position: relative;
  > img {
    height: 200px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
  }
}
 
.hidden-pokemon {
    filter: brightness(0);
}
</style>