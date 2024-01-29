<script setup>
const persons = {
  name: "John Doe",
  country: "United states"
}
</script>

<template>

  <p v-for="person in persons">
    console.log(person)
  </p>

</template>

<style scoped>

</style>