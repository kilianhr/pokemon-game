<script>
export default {
    name: 'PokemonOptions',
    props: {
        pokemons: {
            type: Array,
            required: true
        },
        disabledOptions: {
            type: Boolean,
            required: true
        }
    },
}
</script>

<template>
    <div class="option-container mt-6 d-flex justify-center">
        <ul class="w-75">
            <li v-for="pokemon in pokemons" :key="pokemon.id">
                <v-btn
                    :disabled="disabledOptions"
                    width="100%"
                    @click="$emit('selection', pokemon.id)"
                >
                    {{ pokemon.name }}
                </v-btn>
            </li>
        </ul>
    </div>
</template>

<style scoped>
ul {
    list-style-type: none;
}
li {
    background-color: white;
    border-radius: 5px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
}

li:hover {
    background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
    display: flex;
    justify-content: center;
}
</style>