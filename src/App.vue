<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
body {
  margin: 0;
  padding: 0;

  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    color: #2c3e50;
    padding-top: 2rem;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;

    & > div {
      display: grid;
      grid-column: 2 / 3;

      section {
        margin: 2rem 0;
      }
    }
  }

  .disclaimer {
    border: 1px solid hsl(200, 100%, 25%);
    background: hsl(200, 100%, 90%);
    color: hsl(200, 100%, 25%);
    padding: 0.5rem 1rem;
  }
}
</style>
