<template>
  <div id="app" :class="{'dark-mode': darkMode, 'app-background': true}">

    <header class="header">
      <img :src="darkMode ? require('./assets/logo-dark.svg') : require('./assets/logo.svg')" alt="Logo" class="header-logo" />
      <button @click="toggleDarkMode" class="header-dark-mode-button">
        {{ darkMode ? "Desativar Modo Dark" : "Ativar Modo Dark" }}
      </button>
      <button v-if="selectedRepository" @click="goBack" class="back-button">Voltar</button>
    </header>

    <SearchComponent v-if="!selectedRepository" @search="fetchRepositories" :errorMessage="errorMessage"/>
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
      darkMode: JSON.parse(localStorage.getItem('darkMode')) || false, // Armazena no localStorage
      errorMessage: null, // Nova propriedade para gerenciar a mensagem de erro
    };
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
      localStorage.setItem('darkMode', JSON.stringify(this.darkMode)); // Salva a preferência do usuário
    },
    async fetchRepositories(query) {
      this.errorMessage = null; // Reseta a mensagem de erro antes da nova busca
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
        if (this.repositories.length === 0) {
          this.errorMessage = 'Nenhum repositório encontrado para essa busca.';
        }
      } catch (error) {
        this.errorMessage = 'Erro ao buscar repositórios. Por favor, tente novamente mais tarde.';
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
  min-height: 100vh;
  display: flex;
  justify-content: top;
  align-items: flex-start;
  flex-direction: column;
  padding: 20px;
  color: var(--title-color);
  background-color: var(--background-color); /* Use a variável para a cor de fundo */
  transition: background-color 0.3s;
}

/* Estilos para o modo escuro */
.dark-mode .app-background {
  background-image: none;
  background-color: var(--background-color);
  transition: background-color 0.3s;
}

.header {
  transition: background-color 0.3s;
  background-color: var(--background-color);
  padding: 10px;
  display: flex;
  justify-content: space-evenly;
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
  transition: background-color 0.3s;
  padding: 5px;
  background-color: var(--button-color);
  border: 1px solid var(--border-color);
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  color: var(--text-color);
}

.header-dark-mode-button:hover {
  background-color: var(--button-hover-color);
}

.back-button {
  padding: 5px;
  background-color: var(--button-color);
  border: 1px solid var(--border-color);
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  color: var(--text-color);
}

.back-button:hover {
  background-color: var(--button-hover-color);
}
</style>
