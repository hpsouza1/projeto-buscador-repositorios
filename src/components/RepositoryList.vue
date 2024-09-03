<template>
    <div class="repository-list">
      <RepositoryCard 
        v-for="repo in repos" 
        :key="repo.id" 
        :repo="repo" 
        @repository-selected="handleRepositorySelected"
      />
    </div>
  </template>
  
  <script>
  import RepositoryCard from "./RepositoryCard.vue";
  
  export default {
    name: "RepositoryList",
    components: {
      RepositoryCard,
    },
    props: {
      repos: {
        type: Array,
        required: true
      }
    },
    methods: {
      handleRepositorySelected(repo) {
        this.$emit("repository-selected", repo);
      }
    }
  };
  </script>
  
  <style scoped>
  .repository-list {
    width: 100%;
    display: flex;
    flex-direction: column;
  }
  </style>
  