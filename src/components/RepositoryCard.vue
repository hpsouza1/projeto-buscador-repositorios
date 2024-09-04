<template>
  <div class="repository-card">
    <img :src="repository.avatar" alt="Owner's avatar" class="avatar">
    <div class="info">
      <h2>{{ repository.name }}</h2>
      <p>{{ repository.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RepositoryCard',
  props: {
    repository: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.repository-card {
  display: flex;
  align-items: center;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 15px;
  margin: 10px 0;
  cursor: pointer;
  transition: background-color 0.2s;
}

.repository-card:hover {
  background-color: #f5f5f5;
}

.avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 15px;
}

.info h2 {
  margin: 0;
  font-size: 18px;
  color: #333;
}

.info p {
  margin: 5px 0 0;
  color: #666;
}
</style>
