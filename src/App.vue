<template>
 <div>
   <UserProfile />
 </div>
</template>

<script>
import UserProfile from './components/UserProfile.vue'
export default {
  components: {
    UserProfile
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background: #f3f5fa;
  overflow-x: hidden;
}
</style>
