<template>
    <div class="container">
        <div @click.prevent="changePage" class="btn-corner">
            <i class="far fa-plus-square"></i>
        </div>
        <h1 style="text-align: center; margin-top: 3em; color: #f4900c;">Pokemon List</h1>
        <!-- {{pokemons}} -->
        <div class="container-category"> 
            <Type v-for="(type, i) in types" 
            :key="i"
            :type="type"
            :pokemons="pokemons"
            @fetchPokemon="fetchPokemon"
            @toEditPage="toEditPage"
            @remove="remove"
            ></Type>
        </div>
    </div>
</template>

<script>
import Type from '../components/Type.vue'
export default {
    name: 'HomePage',
    components:{
        Type 
    },
    props: ['types', 'pokemons'], //mewariskan nilai dari parent ke children
    methods:{
        changePage(){
            this.$emit('changePage', 'add-page')
        },
        toEditPage(payload) {
            this.$emit('toEditPage', payload)
        },
        remove(payload) {
            this.$emit('remove', payload)
        },
        fetchPokemon() {
            this.$emit('fetchPokemon')
        }
    }
}
</script>

<style>

</style>