<template>
  
    <form @submit.prevent="handleSubmit">
        <h1>Modifier mon projet</h1>
        <label> Titre </label>
        <input v-model="title" type="text" required >
        <label> Détails </label>
        <textarea v-model="details" required ></textarea>
        <button>Nouveau Projet</button>
    </form>
</template>

<script>
export default {
    name: 'EditProject',
    props: ['id'],
    data(){
        return{
            title: '',
            details: '',
            uri:'http://localhost:3000/projects/' + this.id 
        }
    },
    mounted(){
        fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.title = data.title
                this.details = data.details
            } )
    },
    methods:{
        handleSubmit(){
            fetch(this.uri, {
                method: 'PATCH',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({ title: this.title, details: this.details})

            }).then(() => {
                this.$router.push('/')
            }).catch(err => console.log(err))
        }
    }
}
</script>

<style>

</style>