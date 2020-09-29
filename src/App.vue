<template>
  <div id="app">
    <b-card title="Card Title" no-body>
      <b-card-header header-tag="nav" class="navbar-fixed">
        <b-nav card-header tabs align="center">
          <!-- <b-nav-item>'s with child routes. Note the trailing slash on the first <b-nav-item> -->
          <b-nav-item to="/" exact exact-active-class="active">Home</b-nav-item>
          <b-nav-item to="/categories" exact exact-active-class="active">Categories</b-nav-item>
          <b-nav-item to="/randomizer" exact exact-active-class="active">Randomizer</b-nav-item>
        </b-nav>
      </b-card-header>

      <b-card-body>
        <!-- Child route gets rendered in <router-view> or <nuxt-child> -->
        <router-view></router-view>
        <!-- Or if using Nuxt.js
      <nuxt-child></nuxt-child>
        -->
      </b-card-body>
    </b-card>
  </div>
</template>

<style>
#app {
  font-family: "Rowdies";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

#nav {
  padding: 30px;
}

.nav {
  background: linear-gradient(to right, #9198e5, grey, #9198e5);
}

.nav-item a{
  color: white;
}


#nav a {
  font-weight: bold;
  color: white;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.navbar-fixed {
  position: fixed;
  top: 0;
  width: 100%;
  overflow: hidden;
}


</style>
