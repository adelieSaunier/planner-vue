<template>
  <nav class="filter-nav">
    <!-- je donne comme argument à ma fonction ce par quoi elle doit filtrer -->
    <!-- je bind une classe conditionnelle:la clée est la classe et la valeur est un bool si elle est à true la classe est appliquée -->
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">Voir tous les projets</button>
    <button @click="updateFilter('completed')" :class="{ active: current === 'completed' }">Projets finis</button>
    <button @click="updateFilter('ongoing')" :class="{ active: current === 'ongoing' }">Projets en cours</button>

  </nav>

</template>

<script>
export default {
    name: 'FilterNav',
    methods:{
        updateFilter(by){
            this.$emit('filterChange', by)

        }
    },
    props: ['current']

}
</script>

<style>
.filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}
.filter-nav button.active{
    color: #555;
}

</style>