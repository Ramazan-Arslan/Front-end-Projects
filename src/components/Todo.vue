<template>
  <div class="container">
    <div class="container__header"> {{"TO-DO LIST" }}</div>
    <input class ="container__input-task" type="text" placeholder="Enter a new task" v-model="newTodo"  @keyup.enter="addTodo">
    <div class ="container__task-container" v-for="(todo,index) in todos" :key="todo.id">
        <input class ="container__checkbox"  type="checkbox" v-model="todo.finished">
        <div class ="container__task" :class ="{container__task2:todo.finished == true}" v-if="!todo.edit" @dblclick="edit(todo)">{{todo.task}}</div>
        <input class ="container__editing-task" v-else type="text"  v-model="todo.task" @blur ="editDone(todo)"  @keyup.enter="editDone(todo)">
        <button class ="container__delete-task" @click="removeTodo(index)"><i class="fas fa-trash-alt"></i> </button>
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
      task:'Creating todo app with vue.js',
      finished:true,  
      edit:false,
    },
    {
      id:2,
      task:'Earning $1 million.',
      finished:false,  
      edit:false,
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
          edit:false,

      });
    this.numberOfTask++;
    this.newTodo = '';
    }

    removeTodo(index) {
      this.todos.splice(index, 1);
    }

    edit(todo){
      todo.edit =true

    }

    editDone(todo) {
      todo.edit = false

    }

}
</script>
<style scoped lang="scss">
@import '../style/Todo.scss';
</style>
