<template>
  <div class="hello">
    <p>Hey, checking r/
      <input ref="input" v-on:keydown="onKeyDown" v-if="this.showInput" type="text" v-on:blur="onBlur" v-bind:value="this.msg || this.subreddit">
      <span  v-on:click="onClick" v-else>{{this.msg || this.subreddit}}</span>
    list below!</p>
  </div>
</template>

<script>
export default {
  name: 'DynamicTitle',
  props: ['subreddit', 'inputChanged'],
  data() {
    return {
      msg: '',
      showInput: false,
    }
  },
  created() {

  },
  methods: {
    onBlur(e) {
      this.inputApproved(e);
    },
    onClick() {
      this.showInput = true;
      this.$nextTick(() => {
        this.$refs.input.select();
      })
    },
    onKeyDown(e) {
      if (e.keyCode === 13) {
        this.inputApproved(e);
      }
    },
    inputApproved(e) {
      this.msg = e.target.value;
      this.inputChanged(this.msg);
      this.showInput = false;
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  font-weight: normal;
  font-size: 1.5em;
}
input {
  font-weight: normal;
  font-size: 1em;
  border: none;
  border-bottom: 3px solid grey;
  outline: none;
  width: 200px;
  text-align: center;
}
span {
  font-weight: bold;
  color: #222;
}
</style>
