<template>
  <div class="home">
    <!-- $event represente les données envoyées dans mon by de updateFilter(by) -->
    <FilterNav @filterChange="current = $event" :current="current"/>
    <div v-if="projects.length">
      <!-- filteredProjects me renvoie mon tableau projects[] mais filtrer par états -->
      <div v-for="project in filteredProjects" :key="project.id" >
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />

      </div>
    </div>
   
  </div>
</template>

<script>
// @ is an alias to /src

import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
    
  },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods:{
    //Je verrifie que l'id du projet est égale à celui que je veux supp
    handleDelete(id){
      this.projects = this.projects.filter((project)=> {
        return project.id !== id
      })
    },
    handleComplete(id){
      let proj = this.projects.find(project => {
        return project.id === id
      })
      proj.complete = !proj.complete

    }
  },
  computed: {
    filteredProjects(){
      if(this.current === "completed"){
        return this.projects.filter(project => project.complete)
      }
      if(this.current === "ongoing"){
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
}
</script>
