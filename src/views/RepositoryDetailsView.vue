<!-- src/views/RepositoryDetailsView.vue -->
<template>
    <div>
      <p v-if="!repository">Repositório não encontrado ou carregando...</p>
      <RepositoryDetails v-if="repository" :repo="repository" />
      <RepositoryDetails :repo="repository" />
    </div>
  </template>
  
  <script>
  import RepositoryDetails from '@/components/RepositoryDetails.vue';
  import axios from 'axios';
  
  export default {
    name: 'RepositoryDetailsView',
    components: {
      RepositoryDetails,
    },
    data() {
      return {
        repository: null,
        issues: [],
        errorMessage: null,
      };
    },
    async created() {
      const repoId = this.$route.params.id;
      const storedRepositories = JSON.parse(localStorage.getItem('repositories')) || [];
      this.repository = storedRepositories.find(repo => repo.id === Number(repoId));
      
      if (!this.repository) {
        try {
          const response = await axios.get(`https://api.github.com/repositories/${repoId}`);
          this.repository = response.data;
        } catch (error) {
          console.error('Erro ao buscar o repositório:', error);
        }
      }
    },
  };
  </script>
  