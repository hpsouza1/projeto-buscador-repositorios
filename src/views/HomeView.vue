<template>
  <div class="container">
    <!-- Espaço para a foto -->
    <img src="@/assets/profile2.jpg" alt="Profile Photo" class="profile-photo"/>

    <!-- Informação principal (nome, título, website) -->
    <Info title="Jules Winnfield" text="Hitman"/>
    <p class="website">juleswinnfield.website</p>

    <!-- Botões de contato -->
    <div class="buttons">
      <button class="email-button">
        <i class="fas fa-envelope"></i> Email
      </button>
      <a href="https://www.linkedin.com/in/henrique-pimenta-souza-643b25202/" target="_blank" class="linkedin-link">
        <button class="linkedin-button">
          <i class="fab fa-linkedin"></i> LinkedIn
        </button>
      </a>
      <button @click="toggleTheme" class="toggle-theme-button">
        {{ isDarkMode ? 'Modo Claro' : 'Modo Escuro' }}
        <i :class="isDarkMode ? 'fas fa-sun' : 'fas fa-moon'"></i>
      </button>
    </div>

    <Contact />

    <Socials />
  </div>
</template>


<script>
import Info from '@/components/info.vue';
import Contact from '@/components/contact.vue';
import Socials from '@/components/socials.vue';

export default {
  name: 'Home',
  components: {
    Info,
    Contact,
    Socials
  }
}
</script>

<script>
import Info from '@/components/info.vue';
import Contact from '@/components/contact.vue';
import Socials from '@/components/socials.vue';

export default {
  name: 'Home',
  components: {
    Info,
    Contact,
    Socials
  },
  data() {
    return {
      isDarkMode: true // Tema escuro como padrão
    };
  },
  methods: {
    toggleTheme() {
      this.isDarkMode = !this.isDarkMode;
      this.applyTheme();
      localStorage.setItem('theme', this.isDarkMode ? 'dark' : 'light'); // Armazena a preferência do tema
    },
    applyTheme() {
      const root = document.documentElement;
      if (this.isDarkMode) {
        // Aplica o tema escuro
        root.style.setProperty('--neutral-neutral-700', '#161619');
        root.style.setProperty('--neutral-neutral-600', '#1A1B21');
        root.style.setProperty('--neutral-background', '#23252C');
        root.style.setProperty('--neutral-text', '#FFFFFF');
        root.style.setProperty('--neutral-muted-text', '#C0C0C0');
      } else {
        // Aplica o tema claro
        root.style.setProperty('--neutral-neutral-700', 'var(--background-socials-light)');
        root.style.setProperty('--neutral-neutral-600', 'var(--background-card-light)');
        root.style.setProperty('--neutral-background', 'var(--background-general-light)');
        root.style.setProperty('--neutral-text', 'var(--text-primary-light)');
        root.style.setProperty('--neutral-muted-text', 'var(--text-secondary-light)');
      }
    }
  },
  mounted() {
    const savedTheme = localStorage.getItem('theme');
    this.isDarkMode = savedTheme === 'dark';
    this.applyTheme();
  }
}
</script>

<style scoped>
.container {
  background-color: var(--neutral-neutral-600); 
  max-width: 400px;
  margin: 0 auto;
  padding: 0px;
  border-radius: 8px;
  text-align: center;
  color: var(--neutral-text);
}


.profile-photo {
  width: 100%;
  margin-bottom: 20px;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
}

.website {
  font-size: 12px;
  margin-top: -10px;
  margin-bottom: 20px;
  color: var(--neutral-muted-text);
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
  margin: 10px;
}

.email-button, .linkedin-button{
  padding: 12px 24px; 
  width: 140px; 
  height: 36px;
  border: none;
  border-radius: 6px;
  color: var(--neutral-text); 
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s ease, transform 0.2s ease; 
  display: flex; 
  align-items: center;
  justify-content: center;
}

.email-button {
  background-color: var(--button-email-bg); 
  color: var(--button-text-dark); 
}

.linkedin-button {
  background-color: var(--button-linkedin-bg); 
}

.email-button i, .linkedin-button i {
  margin-right: 8px; 
}

.linkedin-link {
  text-decoration: none; 
}

.toggle-theme-button {
  padding: 12px 24px; 
  width: 140px; 
  height: 36px;
  border: none;
  border-radius: 6px;
  background-color: var(--button-linkedin-bg); 
  color: var(--neutral-text); 
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s ease, transform 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>
