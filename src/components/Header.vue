<template>
  <header class="header">
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
      default: 'This is a title'
    }
  }
}
</script>

<style scoped>
  .header {
    color: #d9d9d9;
    text-align: center;
  }

  h1 {
    font: 50px Verdana, Geneva, Tahoma, sans-serif;
    font-weight: 600;
  }
</style>
