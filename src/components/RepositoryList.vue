<template>
  <div class="repository-list">
    <RepositoryCard
      v-for="repo in repos"
      :key="repo.id"
      :repository="repo"
    />
  </div>
</template>

<script>
import RepositoryCard from './RepositoryCard.vue';

export default {
  name: 'RepositoryList',
  components: {
    RepositoryCard,
  },
  props: {
    repos: {
      type: Array,
      required: true,
    },
  },
};
</script>
  
<style scoped>
.repository-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; /* Centraliza os cards */
  padding: 20px;
  margin-left: 10%;
}

.repository-list > * {
  max-width: 400px; /* Define o comprimento máximo do card */
  width: 100%; /* Faz o card ocupar 100% da largura disponível até o máximo definido */
  margin: 10px;
}
</style>