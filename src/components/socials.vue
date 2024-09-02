<template>
    <div class="socials-container">
      <!-- Links para redes sociais -->
      <a href="https://twitter.com" target="_blank" class="social-icon">
        <i class="fab fa-twitter"></i>
      </a>
      <a href="https://github.com" target="_blank" class="social-icon">
        <i class="fab fa-github"></i>
      </a>
      <a href="https://facebook.com" target="_blank" class="social-icon">
        <i class="fab fa-facebook"></i>
      </a>
      <a href="https://instagram.com" target="_blank" class="social-icon">
        <i class="fab fa-instagram"></i>
      </a>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Socials'
  }
  </script>
  
  <style scoped>
.socials-container {
  padding: 10px;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  gap: 15px;
  background-color: var(--neutral-neutral-700); 
}
  .social-icon {
    color: var(--button-email-bg);
    font-size: 24px;
    text-decoration: none;
  }
  
  .social-icon:hover {
    color: var(--text-highlight); 
  }
  </style>
  