<template>
  <div>
      <input type="text" placeholder="Enter a new task" v-model="newTodo"  @keyup.enter="addTodo">
    <div v-for="(todo,index) in todos" :key="todo.id">
      <div>
        <div v-if="!todo.finished" @dblclick="edit(todo)">{{todo.task}}</div>
        <input v-else type="text"  v-model="todo.task" @blur ="editDone(todo)"  @keyup.enter="editDone(todo)">
      </div>
      <div class="remove-item" @click.native="removeTodo(index)"> 
        &times; 
      </div>
       
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Todo extends Vue {
  @Prop() private msg!: string;
  newTodo='';
  numberOfTask = 3;
  todos=[
      {
      id:1,
      task:'Something will ne done',
      finished:false,  
    },
    {
      id:2,
      task:'Something will be done',
      finished:false,  
    },
  ];


  addTodo() {
    if(this.newTodo.trim() ==''){
      return;
    }
      this.todos.push({
          id:this.numberOfTask,
          task:this.newTodo,
          finished:false,
      });
    this.numberOfTask++;
    this.newTodo = '';
    }

    public removeTodo(index) {
      this.todos.splice(index, 1);
    }

    edit(todo){
      todo.finished =true

    }

    editDone(todo) {
      todo.finished = false

    }

}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
