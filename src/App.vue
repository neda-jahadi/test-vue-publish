<template>
  
      <div id="app">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
        <hr>
        <super-header :isAuthenticated="hasSignedIn" @signOut="hasSignedIn=false" />
        <myContent :isAuthenticated="hasSignedIn" @signOut="handleSignOut()" @signIn="hasSignedIn=true" />
        <Exercise :isPassed="hasPassed" @pass="handlePass()" @reject="handleReject()" />
        <Tourist />
        <ShowApi />
        <!--<div>
          <h1>Api information</h1>
          <ShowApi v-for="srcdata in info" :key="srcdata.id" :srcdata="srcdata"/>
        </div>-->
      </div>
  
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import myContent from './components/myContent.vue'
import Header from './components/Header'
import Exercise from './components/Exercise'
import Tourist from './components/Tourist'
import ShowApi from './components/ShowApi'

//import axios from 'axios'
window.axios = require('axios');
export default {
  name: 'App',
 // mounted: function() {
    //axios.get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?latest')
    //.then(response=>(this.info=response.data))
  //},
  components: {
    HelloWorld,
     myContent,
     'super-header':Header,
     Exercise,
     Tourist,
     ShowApi
  },
 
  data:()=>({
    hasSignedIn: false,
    hasPassed: false,
    info: null
  }),
  methods: {
    handleSignOut(){ this.hasSignedIn=false;},
    handlePass(){this.hasPassed=true;},
    handleReject(){this.hasPassed=false;}
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  
}
</style>
