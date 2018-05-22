<template>
  <footer class="footer">
    <span>Written by {{ author }}</span>
  </footer>
</template>

<script>
export default {
  props: {
    author: {
      type: String,
      default: 'Anonymous'
    }
  },
}
</script>

<style scoped>
  .footer {
    color:#063;
    font-size: small;
    text-align: center;
    padding-top: 20px;
  }
</style>
