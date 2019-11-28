<template>
  <div id="app" style="background-color: #343536;">
    <div style="background-color: black;">
      <div class="logo">
        <br>
        <br>
        <div class="ml-5 ">
          <h1 class="pb-0">CineSafari</h1>
        </div>
      </div>
      <div class="text-center pt-0" id="nav">
        <router-link to="/">Home </router-link> 
        <router-link v-if="!nowuser" to="/login">| login </router-link>
        <router-link v-if="!nowuser" to="/signup">| signup </router-link>
        <span id="logout" v-if="nowuser" @click="logout">| logout </span>
        <router-link v-if="nowuser" to="/userPage">| {{userName}} </router-link> 
      </div>
    </div>
    <div class="mt-4">
      <router-view :key="$route.fullpath"/>
    </div>
  </div>
</template>

<script>
import jwtDecode from "jwt-decode"
export default {
  data(){
    return {
      nowuser: this.$session.has('jwt'),
      userName: ""
    }
  },
  methods: {
    logout(){
      this.nowuser = false
      this.$session.destroy();
      this.$router.push('/');
    },
    userNameFind(){
      if (this.nowuser){
        const token = this.$session.get('jwt')
        const decodedToken = jwtDecode(token)
        this.userName = decodedToken.username
      }
    }
  },
  updated(){
    this.nowuser = this.$session.has('jwt'),
    this.userNameFind()
  },
  mounted(){
    this.nowuser = this.$session.has('jwt'),
    this.userNameFind()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: white;
}

.logo {
  font-weight: bold;
  font-family: 'Courier New', Courier, monospace; 
  color: white;
}

#nav {
  padding: 30px;
}

#nav a {
  font-size: 17px;
  font-weight: bold;
  color: #8aa4be;
}
#logout {
  font-size: 17px;
  font-weight: bold;
  color: #8aa4be;
}

#nav a.router-link-exact-active {
  font-size: 20px;
  color: #f8faf9;
}
</style>
