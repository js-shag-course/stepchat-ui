<template>
  <div>
    <div v-for="(user, i) in users" :key="i" >{{ user }}</div>
  </div>
</template>

<script>
export default {
  name: 'Users',
  props: {
    users: Array
  }
}
</script>
