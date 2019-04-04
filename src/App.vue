<template>
  <div id="app">
    <div id="nav">
      <router-link to="/demo">DemoD3</router-link>  | <router-link to="/barchart">Barchart</router-link>  | <router-link to="/about">Scatterplot</router-link>  | <router-link to="/about">HeatMap</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
