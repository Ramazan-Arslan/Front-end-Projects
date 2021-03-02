<template>
  <div id="app">
    <Todo/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Todo from './components/Todo.vue';

@Component({
  components: {
    Todo,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  text-align: center;
  margin-top: 10%;
  margin-left:20%;
  margin-right:20%;
}
</style>
