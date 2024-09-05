<template>
  <div id="app" :class="{'dark-mode': darkMode, 'app-background': true}">
    <header class="header">
      <img :src="darkMode ? require('./assets/logo-dark.svg') : require('./assets/logo.svg')" alt="Logo" class="header-logo" />
      <button @click="toggleDarkMode" class="header-dark-mode-button">
        {{ darkMode ? "Desativar Modo Dark" : "Ativar Modo Dark" }}
      </button>
      <button v-if="selectedRepository" @click="goBack" class="back-button">Voltar</button>
    </header>

    <SearchComponent v-if="!selectedRepository" @search="fetchRepositories" />
    <RepositoryList v-if="!selectedRepository && repositories.length" :repos="repositories" @repository-selected="showRepositoryDetails" />
    <RepositoryDetails v-if="selectedRepository" :repo="selectedRepository" @go-back="goBack" />
  </div>
</template>

<script>
import axios from 'axios';
import SearchComponent from './components/SearchComponent.vue';
import RepositoryList from './components/RepositoryList.vue';
import RepositoryDetails from './components/RepositoryDetails.vue';

export default {
  name: 'App',
  components: {
    SearchComponent,
    RepositoryList,
    RepositoryDetails,
  },
  data() {
    return {
      repositories: [],
      selectedRepository: null,
      darkMode: false,
    };
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
    },
    async fetchRepositories(query) {
      try {
        const response = await axios.get(`https://api.github.com/search/repositories?q=${query}`);
        this.repositories = response.data.items.map(repo => ({
          id: repo.id,
          name: repo.full_name,
          description: repo.description,
          avatar: repo.owner.avatar_url,
          stars: repo.stargazers_count,
          forks: repo.forks,
          openIssues: repo.open_issues,
        }));
      } catch (error) {
        console.error('Erro ao buscar repositórios:', error);
      }
    },
    showRepositoryDetails(repo) {
      this.selectedRepository = repo;
    },
    goBack() {
      this.selectedRepository = null;
    },
  },
};
</script>
  
<style scoped>
.app-background {
  background-image: url("./assets/github-background.svg");
  background-size: 50%;
  background-repeat: no-repeat;
  background-position: right;
  min-height: 100vh;
  display: flex;
  justify-content: top;
  align-items: flex-start;
  flex-direction: column;
  padding: 20px; /* Espaçamento das bordas */
  color: var(--title-color);
}

/* Estilos para o modo escuro */
.dark-mode .app-background {
  background-image: none; /* Remove a imagem de fundo */
  background-color: #1a1a1a;
}

.header {
  background-color: var(--header-background-color);
  padding: 10px;
  display: flex;
  justify-content: space-evenly; /* Ajustando a posição dos elementos */
  align-items: center;
  width: 100%;
}

.header-logo {
  max-width: 150px;
  height: auto;
}

.header-title {
  margin: 0;
  font-size: 1.5rem;
  color: var(--title-color);
}

.header-dark-mode-button {
  padding: 5px;
  background-color: var(--button-color);
  border: 1px black none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  color: var(--text-color);
}

.header-dark-mode-button:hover {
  background-color: var(--button-hover-color); /* Cor do botão ao passar o mouse */
}
</style>
