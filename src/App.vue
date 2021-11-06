<template>
  <div id="wrapper">
    <nav class='navbar is-dark'>
      <div class='navbar-brand'>
        <router-link to='/' class='navbar-item'><strong>Cores</strong></router-link>
      </div>
    </nav>
  

    <section class='section'>
      <router-view/>
    </section>

    <footer class='footer'>
        <p class='has-text-centered'> Copyright (c) 2021</p>
    </footer>

  </div>
</template>

<style lang="scss">
@import '../node_modules/bulma';
</style>
