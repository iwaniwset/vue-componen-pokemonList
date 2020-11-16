<template>
      <section id="main">
        <div class="btn-corner">
            <i class="far fa-plus-square"></i>
        </div>
        <HomePage
            v-if="pageName == 'home-page'"
            :types="types"
            :pokemons="pokemons"
            @changePage="changePage"
            @toEditPage="toEditPage"
            @remove="remove"
            @fetchPokemon="fetchPokemon"
            ></HomePage>
        <AddPage
            v-else-if="pageName == 'add-page'"
            @addStudent="addStudent">
            </AddPage>
        <EditPage
            v-else-if="pageName == 'edit-page'"
            :pokemonDetail="pokemonDetail"
            @editData="editData"
            ></EditPage>

        <!-- MAIN CONTAINER -->
        
    </section>

</template>

<script>
import HomePage from './views/HomePage.vue'
import AddPage from './views/AddPage.vue'
import EditPage from './views/EditPage.vue'
import axios from './config/axios'
export default {
    name: 'App',
    components: {
        HomePage, AddPage, EditPage
    },
    data() {
        return{
            pageName: "home-page",
            types: [
                {
                    type: 'Electric',
                    icon: '⚡',
                    color: 'yellow'
                },
                {
                    type: 'Grass',
                    icon: '🌿',
                    color: 'green'
                },
                {
                    type: 'Fire',
                    icon: '🔥',
                    color: 'red'
                },
                {
                    type: 'Water',
                    icon: '💧',
                    color: 'blue'
                }
            ],
            pokemons: [],
            pokemonDetail: {}
            

        }
    },
    methods:{
        fetchPokemon(){
            axios({
                url: '/pokemons',
                method: 'get'
            })
            .then(({data})=>{
                // console.log(data, '<<<<<<<< ini data');
                this.pokemons = data
            })
            .catch(err =>{
                console.log(err.response, '<<<<< error fetch' );
            })
        },
        changePage(name) {
            this.pageName = name
        },
        addStudent(payload){
            axios({
                url: '/pokemons',
                method: "POST",
                data:{
                    name: payload.name,
                    img: payload.img,
                    type: payload.type
                }
            })
            .then(({data})=>{
                Swal.fire(
                    'Added data Sucessfully!',
                    'success'
                )
                // this.pokemons.push(data)
                this.fetchPokemon()
                this.changePage('home-page')
            })
            .catch(err=>{
                console.log(err.response, '<<<<<< error add data');
            })
                
        },
        toEditPage(pokemon){
            this.changePage('edit-page')
            this.pokemonDetail = pokemon
        },
        editData(payload) {
            axios({
                url: `/pokemons/${payload.id}`,
                method: 'PUT',
                data: {
                    name: payload.name,
                    img: payload.img,
                    type: payload.type
                }
            })
            .then(({data})=>{
                Swal.fire(
                    'Updated Sucessfully!',
                    'success'
                )
                this.fetchPokemon()
                this.changePage('home-page')
            })
            .catch(err => {
                console.log(err.response, 'err edit')
            })
        },
        remove(id) {
             Swal.fire({
                title: "Are you sure to delete this pokemon?",
                icon: "warning",
                showCancelButton: true,
                confirmButtonColor: "#3085d6",
                cancelButtonColor: "#d33",
                confirmButtonText: "Yes, delete it!",
            })
             .then((result) => {
                if (result.isConfirmed) {
                    return axios ({
                        url: `/pokemons/${id}`,
                        method: 'delete'
                    })
                }
             })
            .then((data)=>{
                this.fetchPokemon()
            })
            .catch(err=>{
                console.log(err.response, '<<<<< error delete');
            })
        }
    },
    created(){
        this.fetchPokemon()
    }


}
</script>

<style>

</style>