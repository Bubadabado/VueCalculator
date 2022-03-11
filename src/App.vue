<template>
  <div id="app">
    <div id="pageContent">
      <div class="page-content">
        <div class="header">
          <h1>Calculator App</h1>
          <nav>
            <router-link to="/">Home</router-link>
            <router-link to="/calculator">Calculator</router-link>
            <router-link to="/history">History</router-link>
          </nav>
        </div>
        <router-view/>
      </div>

      <div id="pageFooter">
          <p>Created by Adam Robertson. <a href="https://github.com/Bubadabado/VueCalculator">Github Repository</a></p>
      </div>
    </div>
  </div>
</template>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
  padding: 0;
}

div.page-container {
  position: relative;
  min-height: 100vh;
}
div.page-content {
  position: relative; 
  padding-bottom: 3.5rem;
}

.header {
  background-color: rgb(36, 33, 41);
  padding: 6px;
  margin-bottom: 32px;
}

.header h1 {
  color: rgb(255, 255, 255);
}

nav {
  padding: 30px;
}

nav a {
  background-color: rgb(119, 47, 42);
  padding: 16px;
  margin: 10px;
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
  color: rgb(177, 177, 177);
}

nav a.router-link-exact-active {
  color: white;
}

#pageFooter {
    /* position: absolute; */
    position: fixed;
    padding-bottom: 1px;
    background-color: rgb(211, 208, 216);
    bottom: 0;
    width: 100%;
    text-align: center;
}

</style>
