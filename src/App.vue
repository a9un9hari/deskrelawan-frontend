<template>
  <div id="app" class="container mx-auto">
    <ul class="flex">
      <li class="mr-6">
        <router-link to="/" active-class="font-bold" class="text-blue-500 hover:text-blue-800">Home</router-link>
      </li>
      <li class="mr-6">
        <router-link to="/login"  active-class="font-bold" class="text-blue-500 hover:text-blue-800">Login</router-link>
      </li>
      <li class="mr-6">
        <router-link to="/about"  active-class="font-bold" class="text-blue-500 hover:text-blue-800">Register</router-link>
      </li>
    </ul>
    <router-view/>
  </div>
</template>
<script>
export default {
  name: 'App'
}
</script>

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
