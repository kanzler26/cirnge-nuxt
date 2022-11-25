<template>
  <section>
    <h1>Users Page</h1>
    <ul>
      <li v-for="user of 5" :key="user">
        <a @click.prevent="openUser(user)" href="#">User {{ user }}</a>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  methods: {
    openUser(num) {
      this.$router.push('/users/' + num)
    }
  }
}
</script>
