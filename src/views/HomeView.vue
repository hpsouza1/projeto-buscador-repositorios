<template>
  <div>
    <!-- Barra de Busca -->
    <SearchComponent />

    <!-- Feedback de Repositório Não Encontrado -->
    <FeedbackComponent v-if="showFeedback" />

    <!-- Lista de Repositórios -->
    <RepositoryList v-if="repositories.length > 0" :repositories="repositories" />
  </div>
</template>

<script>
import SearchComponent from '@/components/SearchComponent.vue'
import FeedbackComponent from '@/components/FeedbackComponent.vue'
import RepositoryList from '@/components/RepositoryList.vue'

export default {
  components: {
    SearchComponent,
    FeedbackComponent,
    RepositoryList
  },
  data() {
    return {
      repositories: [],  // Aqui você vai armazenar os repositórios buscados
      showFeedback: false // Controle para exibir feedback se necessário
    };
  },
  methods: {
    // Métodos para lidar com a busca, atualização da lista de repositórios e feedback
  }
}
</script>
