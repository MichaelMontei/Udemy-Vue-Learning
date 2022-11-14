<template>
<FriendContact
  name="Michael Monteiro"
  phone-number="12345 5678 899"
  email-address="michael@localhost.com"
></FriendContact>


</template>

<script>
import FriendContact from './components/FriendContact.vue';

export default {
  name: 'App',
  components: {
    FriendContact,
  },
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
