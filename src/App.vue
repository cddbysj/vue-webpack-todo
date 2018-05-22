<template>
  <div id="app">
    <Header :title="title"></Header>
    <Todo></Todo>
    <Footer :author="author"></Footer>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Todo from './components/Todo.vue'
import Footer from './components/Footer.vue'

export default {
  data() {
    return {
      title: 'Todos',
      author: '©Bill Wen'
    }
  },
  components: {
    Header,
    Todo,
    Footer
  }
}
</script>

<style>
  body {
    max-width: 800px;
    color: rgb(114, 138, 66);
    background: #fff;
    margin: 10% auto;
    box-sizing: border-box;
  }
</style>
