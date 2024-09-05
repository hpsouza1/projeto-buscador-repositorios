<template>
  <div class="repository-card" @click="selectRepository">
    <img :src="repository.avatar" alt="Repository Avatar" class="avatar" />
    <h2>{{ repository.name }}</h2>
    <p>{{ repository.description }}</p>
    <p>Stars: {{ repository.stars }} | Forks: {{ repository.forks }} | Issues: {{ repository.openIssues }}</p>
  </div>
</template>

<script>
export default {
  name: 'RepositoryCard',
  props: {
    repository: {
      type: Object,
      required: true
    }
  },
  methods: {
    selectRepository() {
      this.$emit('repository-selected', this.repository);
    }
  }
}
</script>

<style scoped>
.repository-card {
  cursor: pointer;
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.repository-card:hover {
  background-color: #f9f9f9;
}

.avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
</style>
