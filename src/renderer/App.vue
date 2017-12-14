<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'inovafarma-sorteio'
  }
</script>

<style lang="scss">
#app > .el-row {
  position: relative;
  z-index: 2;
}
  .modules{
    height: 100%;
  }
  @keyframes fadein {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  body > div {
    -webkit-user-select: none;
  }
  body, html {
    height: 100%;
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: BlinkMacSystemFont, -apple-system, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    .container-panel > *{
      cursor: default;
    }
    /* Disable text selection, or your app will feel like a web page */
    -webkit-user-select: none;
    // -webkit-app-region: drag;   // Specifies only where it would be able to drag.
    // Or put 'no-drag' inside items that can be clicked

    /* Cover the whole window */
    height: 100%;

    /* Make sure this matches the native window background color that you pass to
    * electron.BrowserWindow({...}), otherwise your app startup will look janky. */
    background: #E3EFF6;

    /* Smoother startup */
    animation: fadein 0.5s;
  }
  /**
  * Change style of all scrollbar
  */
  *::-webkit-scrollbar {
    width: 9px;
  }
  *::-webkit-scrollbar-thumb {
    border-radius: 200px;
    background-color: #d9d9de;
  }
  *::-webkit-scrollbar-track {
    background-color: #f3f3f3;
  }
</style>
