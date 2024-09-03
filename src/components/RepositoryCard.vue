<template>
    <div class="repository-card" @click="handleClick">
      <img :src="repo.avatar" alt="Avatar" class="repository-avatar" />
      <div class="repository-info">
        <h3 class="repository-title">{{ repo.name }}</h3>
        <p v-if="repo.description" class="repository-description">{{ repo.description }}</p>
      </div>
      <div class="repository-arrow">
        ➔
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "RepositoryCard",
    props: {
      repo: {
        type: Object,
        required: true
      }
    },
    methods: {
      handleClick() {
        this.$emit("repository-selected", this.repo);
      }
    }
  };
  </script>
  
  <style scoped>
  .repository-card {
    display: flex;
    align-items: center;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    padding: 15px;
    margin: 10px 0;
    cursor: pointer;
    transition: background-color 0.2s;
  }
  
  .repository-card:hover {
    background-color: #f9f9f9;
  }
  
  .repository-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 15px;
  }
  
  .repository-info {
    flex: 1;
  }
  
  .repository-title {
    margin: 0;
    font-size: 1.25rem;
    color: #333;
  }
  
  .repository-description {
    margin: 5px 0 0 0;
    font-size: 0.875rem;
    color: #666;
  }
  
  .repository-arrow {
    font-size: 1.5rem;
    color: #ccc;
  }
  </style>
  