<template>
  <div class="container">
    <div class="container__header"> {{"TO-DO LİST" }}</div>
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container{
  background: #FFFFFF;
  border: 1px solid #E2E1E1;
  box-shadow: 2px 2px 4px rgba(215, 215, 215, 0.5);
  border-radius: 8px;
  font-family: sans-serif;
  

  &__header{
    border: 1px solid #E2E1E1;
    box-shadow: 2px 2px 4px rgba(215, 215, 215, 0.5);
    font-size: 30px;
    line-height: 36px;
    padding: 1.5%;
    color: #333333;

  }
  &__input-task{
    border: 1px solid #E2E1E1;
    box-shadow: 2px 2px 4px rgba(215, 215, 215, 0.5);
    border-radius: 8px;
    width: 68%;
    font-size: 20px;
    line-height: 24px;
    text-align: center;
    color: #333333;
    margin-top: 3%;
    margin-bottom: 3%;
    padding: 1%;
  }

  &__task-container{
    display: grid;
    grid-template-columns: 15% 45px auto 10px 45px 15%;
    margin-bottom: 2%;
   
  }
  &__checkbox{
    grid-column: 2/3;
    width: 80%;
    height: 80%;
    
   

    
  }
  &__task{
    grid-column: 3/4;
    background: #F9F9F9;
    border: 1px solid #E2E1E1;
    box-shadow: 2px 2px 4px rgba(215, 215, 215, 0.5);
    border-radius: 8px;
    font-size: 12px;
    font-weight: 600;
    padding: 3%;
    color: #333333;

  }
  &__task2{
    font-style: italic;
    text-decoration: line-through;
    color:grey;

  }
  &__delete-task{
    grid-column: 5/6;
    color:#FFFFFF;
    background: #C41D1D;
    border: none;
    border-radius: 16%;
    cursor: pointer;
    &:hover{
      background-color:gray; 
      width: 103%;
      height: 103%;
    }
    
  }

  &__editing-task{
    grid-column: 3/4;
    background: #F9F9F9;
    border: 1px solid #E2E1E1;
    box-shadow: 2px 2px 4px rgba(215, 215, 215, 0.5);
    border-radius: 8px;
    font-size: 12px;
    font-weight: 600;
    padding: 3%;
    color: #333333;
    text-align: center;
     &:enabled{
      background-color:white ;
    }

  
  }
}

</style>
