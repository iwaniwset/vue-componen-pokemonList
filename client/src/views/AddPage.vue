<template>
    <!-- ADD FORM -->
        <div class="addForm"> 
            <div class="addForm-container">
                <div class="addForm-head">
                    <h3>Add New Pokemon</h3>
                </div>
                <form @submit.prevent="addStudent" class="addForm-body">
                    <div class="nes-field">
                        <label for="name_field">
                            <i class="fas fa-comment-medical"></i>
                            Pokemon Name
                            </label>
                        <input v-model="name" type="text" id="name_field" class="nes-input">
                    </div>
                    <div class="nes-field" style="margin-top: 20px;">
                        <label for="name_field"><i class="fas fa-camera-retro"></i>
                        Image_Url
                        </label>
                        <input v-model="img" type="text" id="name_field" class="nes-input">
                    </div>
                    <label for="phase" style="margin-top: 20px;">Select Type</label>
                    <div class="nes-select">
                        <select v-model="selected" id="phase" name="phase">
                            <option value="" disabled selected hidden>Select...</option>
                            <option value="Electric">⚡ Electric</option>
                            <option value="Grass">🌿 Grass</option>
                            <option value="Fire">🔥 Fire</option>
                            <option value="Water">💧 Water</option>
                        </select>
                    </div>
                    <div class="addForm-button">
                        <button type="submit" class="nes-btn is-success">Add Pokemon</button>
                    </div>
                </form>
            </div>
        </div>
</template>

<script>
export default {
    name: 'AddPage',
    data(){
        return{
            name: '',
            img: '',
            selected:''
        }
    },
    methods:{
        addStudent(){
            let payload = {
                name: this.name,
                img: this.img,
                type: this.selected

            }
            this.$emit('addStudent', payload)
        }
    }

}
</script>

<style>

</style>