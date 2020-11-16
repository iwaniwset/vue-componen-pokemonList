<template>
    <div class="card" :class="`card-${type.color}`">
        
        <!-- {{pokemon}} -->
        <div class="card-img">
            <img :src="pokemon.img" alt="image" />
        </div>
        <div class="card-body">
            <!-- {{pokemon.name}} -->
            <p>{{pokemon.name}}</p>
        </div>
        <div class="card-button">
            <i @click.prevent="toEditPage" class="fas fa-pen-square"></i>
            <i @click.prevent="remove"  class="fas fa-minus-square"></i>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Pokemon',
    props: ['pokemon', 'type'],
    methods:{
        toEditPage() {
            this.$emit('toEditPage', this.pokemon)
        },
        remove() {
            this.$emit('remove', this.pokemon.id)
        }
    }
}
</script>

<style>

</style>