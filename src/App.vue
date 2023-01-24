<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Echo from "laravel-echo"

window.Pusher = require('pusher-js');

window.Echo = new Echo({
  broadcaster: 'pusher',
  key: "websocketkey",
  wsHost: "rust-dev-socket.powerit.dev",
  wsPort: 6001,
  cluster:"mt1",
  forceTLS: true,
  disableStats: true,
});

window.Echo.channel(`my-channel`)
    .listen('.my-event', (e) => {
      console.log(e);
      console.log('Test');
    });

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
