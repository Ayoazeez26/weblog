<template>
  <div id="app">
    <div class="nav">
      <ul class="nav-ul">
        <li>WeBlog</li>
        <li><router-link :to="'/'">Home</router-link></li>
      </ul>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}

.nav {
  position: fixed;
  top: 0;
  width: 100%;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  background-color: #0B5F73;
  color: white;
  font-size: 24px;
  z-index: 99;
}

.nav-ul {
  display: flex;
  justify-content: flex-start;
}

.nav-ul li {
  list-style-type: none;
  color: white;
  width: 100px;
}

@media screen and (max-width: 768px) {
  .nav {
    height: 40px;
  }
  .nav-ul:first-child {
    font-size: 20px;
  }
  .nav-ul li{
    width: auto;
    margin-right: 20px;
  }
}
</style>
