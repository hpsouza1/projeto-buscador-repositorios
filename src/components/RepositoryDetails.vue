<template>
    <div class="repository-details">
      <div class="repository-header">
        <img :src="repo.avatar" alt="Repository Avatar" class="avatar" />
        <h1>{{ repo.name }}</h1>
        <p>{{ repo.description }}</p>
      </div>
      <div class="repository-kpis">
        <div class="kpi">
          <h3>Stars</h3>
          <p>{{ repo.stars }}</p>
        </div>
        <div class="kpi">
          <h3>Forks</h3>
          <p>{{ repo.forks }}</p>
        </div>
        <div class="kpi">
          <h3>Issues</h3>
          <p>{{ repo.openIssues }}</p>
        </div>
      </div>
      <div class="issue-list">
        <div v-for="issue in issues" :key="issue.id" class="issue-card">
          <a :href="issue.html_url" target="_blank" class="issue-link">
            <h3>{{ issue.title }}</h3>
            <p>{{ issue.body }}</p>
          </a>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'RepositoryDetails',
    props: {
      repo: Object
    },
    data() {
      return {
        issues: []
      };
    },
    async created() {
      await this.fetchIssues();
    },
    methods: {
      async fetchIssues() {
        try {
          const response = await axios.get(`https://api.github.com/repos/${this.repo.name}/issues`);
          this.issues = response.data;
        } catch (error) {
          console.error('Erro ao buscar issues:', error);
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .repository-details {
    padding: 20px;
  }
  
  .repository-header {
    text-align: center;
    margin-bottom: 20px;
  }
  
  .avatar {
    width: 100px;
    height: 100px;
    border-radius: 50%;
  }
  
  .repository-kpis {
    display: flex;
    justify-content: space-around;
    margin-bottom: 20px;
  }
  
  .kpi {
    text-align: center;
  }
  
  .issue-list {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }
  
  .issue-card {
    border: 1px solid #ddd;
    padding: 20px;
    border-radius: 5px;
    width: 100%;
    max-width: 300px;
  }
  
  .issue-link {
    text-decoration: none;
    color: inherit;
  }
  
  .issue-card:hover {
    background-color: #f9f9f9;
  }
  </style>
  