<template>
    <div class="category">
        <div class="category-head"
        :class="`category-${type.color}`">
            <h3>{{type.type}}</h3>
            <h3>{{type.icon}}</h3>
        </div>
        <div class="category-body">
            <!-- {{pokemons}} -->
            <!-- {{pokemonsPerType}} -->
            <draggable 
            :list="pokemonsPerType" group="pokemon" 
            :move="onMove"
            :type="type"
            @end="updateType">
            <Pokemon
                v-for="pokemon in pokemonsPerType" 
                :key="pokemon.id"
                :pokemon="pokemon"
                :type="type"
                :id="pokemon.id"
                @toEditPage="toEditPage"
                @remove="remove"
                >
            </Pokemon>
            </draggable>
            
        </div>
    </div>
</template>

<script>
import Pokemon from './Pokemon'
import draggable from 'vuedraggable'
import axios from '../config/axios'
export default {
    name: 'Type',
    data(){
        return {
            currentId: null,
            currentType: null
        }
    },
    components: {
        Pokemon, draggable
    },
    props: ['type', 'pokemons'],
    computed: {
        pokemonsPerType(){
            return this.pokemons.filter(pokemon => pokemon.type == this.type.type)
        }
    },
    methods:{
        toEditPage(payload){
            this.$emit('toEditPage', payload)
        },
        remove(payload) {
            this.$emit('remove', payload)
        },
        updateType() {
            axios ({
                url: `/pokemons/${this.currentId}`,
                method: 'patch',
                data: {
                    type: this.currentType
                }
            })
            .then(()=>{
                this.$emit('fetchPokemon')
            })
            .catch(err=>{
                console.log(err.response, '<<<<<<< err draggable');
            })
        },
        onMove(evt) {
            // console.log(evt);
            console.log(evt.draggedContext.element.id, "<<<<<<< ini id");
            console.log(evt.relatedContext.component.$attrs.type.type, "ini current Type");
            this.currentId = evt.draggedContext.element.id
            this.currentType = evt.relatedContext.component.$attrs.type.type
        }

    }

}
</script>

<style>

</style>