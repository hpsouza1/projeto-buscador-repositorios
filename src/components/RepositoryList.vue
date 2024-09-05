<template>
  <div class="repository-list">
    <div v-for="repo in repos" :key="repo.id" class="repository-card" @click="selectRepository(repo)">
      <img :src="repo.avatar" alt="Repo Avatar" class="repo-avatar" />
      <h2>{{ repo.name }}</h2>
      <p>{{ repo.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RepositoryList',
  props: {
    repos: Array
  },
  methods: {
    selectRepository(repo) {
      this.$emit('repository-selected', repo);
    }
  }
}
</script>

<style scoped>
.repository-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.repository-card {
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.repository-card:hover {
  background-color: #f5f5f5;
}

.repo-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
</style>
