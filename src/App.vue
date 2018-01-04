<template>
  <div id="app">
    <img src="https://image.flaticon.com/icons/svg/141/141836.svg">
    <DynamicTitle/>
    <VerticalList v-bind:subreddit="this.subreddit"/>
  </div>
</template>

<script>
import DynamicTitle from './components/DynamicTitle'
import VerticalList from './components/VerticalList'

export default {
  name: 'app',
  components: {
    DynamicTitle,
    VerticalList,
  },
  data() {
    return {
      subreddit: ''
    }
  },
  methods: {
    inputChanged(subreddit) {
      this.subreddit = subreddit;
    }
  },
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
img {
  width: 10vh;
}
</style>
