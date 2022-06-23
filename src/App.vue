<template>
  <html>
    <header>
      <div id="logo">
        logo
      </div>
      <div id="logoTitle">
        SephirPro
      </div>
    </header>

    <main>
      <router-view />
      <!---<TheWelcome />-->
    </main>
  </html>
</template>

<style>
@import './assets/base.css';
</style>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
