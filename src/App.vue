<template>
  <div id="app" class="app-background">
    <header class="header">
      <h1 class="header-title">Github Explorer</h1>
      <button @click="toggleDarkMode" class="header-dark-mode-button">
        {{ darkMode ? "Desativar Modo Noturno" : "Ativar Modo Noturno" }}
      </button>
    </header>
    <SearchComponent @search="fetchRepositories" />
    <RepositoryList 
      v-if="repositories.length" 
      :repos="repositories" 
      @repository-selected="showRepositoryDetails"
    />
  </div>
</template>

<script>
import SearchComponent from "./components/SearchComponent.vue";
import RepositoryList from "./components/RepositoryList.vue";

export default {
  name: "App",
  components: {
    SearchComponent,
    RepositoryList,
  },
  data() {
    return {
      darkMode: false,
      repositories: []
    };
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
      // Aqui você pode alternar as cores para o modo noturno posteriormente
    },
    fetchRepositories(query) {
      // Repositório mockado
      this.repositories = [
        {
          id: 1,
          name: "vuejs/vue",
          description: "The Progressive JavaScript Framework",
          avatar: "https://avatars.githubusercontent.com/u/6128107?v=4",
        }
      ];
    },
    showRepositoryDetails(repo) {
      console.log("Repositório selecionado:", repo);
      // Lógica para mostrar os detalhes do repositório selecionado
    }
  }
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

.header {
  background-color: var(--header-background-color);
  padding: 10px;
  display: flex;
  justify-content: space-evenly; /* Ajustando a posição dos elementos */
  align-items: center;
  width: 100%;
}

.header-title {
  margin: 0;
  font-size: 1.5rem;
  color: var(--title-color);
}

.header-dark-mode-button {
  padding: 5px;
  background-color: transparent;
  border: 1px black none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  color: var(--title-color);
}

.header-dark-mode-button:hover {
  background-color: #21f37c; /* Cor do botão ao passar o mouse */
}
</style>
