<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/Favorites">Favorites</router-link> |
      <router-link to="/Find">Find</router-link> |
      <router-link to="/Add">Add</router-link>
    </div>
    <router-view/>
  <!--<p> {{GetFirstItem}} </p>-->
  <div class="footer-names">
          <p>Keifer Higham, Katie Rencher</p>
</div>


  <div class="github-footer-fixed"><a href='https://github.com/ktrencher/CreativeProject4'><img src='../images/github-dark.svg' /></a></div>
  </div>

</template>



<script>
export default {

  computed: {

    numCartItems () {
      const numItems = this.$root.$data.numItems
      return numItems
    },
    GetFirstItem () {
    return this.$root.$data.Movies[0]
    },

  },

  }

</script>

<style>
body {
  background-color: #d4e0fa;
}

.github-footer-fixed {
user-select: none;
width: 40px;
height: 40px;
position: fixed;
right: 2vh;
bottom: 2vh;
font-size: 25%;
}


.footer-names {
position: fixed;
right: 10vh;
bottom: 2vh;
font-size: 25%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
  font-size: 45px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

@media only screen and (max-width:401px) {
  #nav {
    font-size: 20px;
  }
}
</style>
