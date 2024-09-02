<template>
    <div class="contact-info">
      <div class="centralizando">
        <h2>About</h2>
      <p>
        I'm Jules Winnfield. I've done things I ain't too proud of. But now, I'm tryingin' to be a righteous man, a shepherd guiding the weak through the valley of darkness. I ain't perfect, but I'm workin' on it, one step at a time.  
      </p>
  
      <h2>Interests</h2>
      <p>
        Preacher of redemption. Lover of the Old Testament. Burger enthusiast. And always ready for a good debate on what Ezekiel 25:17 really means.
      </p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Contact'
  }
  </script>
  
  <style scoped>
  .centralizando{
    padding-left: 10%;
    padding-right: 10%; 
    margin-top: 10%;
    margin-bottom: 10%;
    height: 270px;
    color: var(--neutral-muted-text);
  }

  .contact-info {
  background-color: transparent;
  text-align: left;
  margin-bottom: 20px;
}
  
  .contact-info h2 {
    margin-top: 20px;
    margin-bottom: 10px;
    font-size: 18px;
  }
  
  .contact-info p {
    font-size: 14px;
    line-height: 1.6;
    color: var(--neutral-muted-text);
  }
  </style>
  