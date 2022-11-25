<template>
  <section>
    <!-- <h1>User {{ $route.params.id }}</h1> -->
    <h1>test show or not</h1>

  </section>
</template>

<script>
export default {
  validate() {
    console.log('validate')
    return true
  },
}
</script>