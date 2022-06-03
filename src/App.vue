<template>
  <div id="app">
    <h1>todos</h1>
    <div class="text-field">
      <v-form @submit.prevent="addTodo(mydata)">
    <v-text-field  v-model="mydata"></v-text-field>
    </v-form>
  </div>
  <ItemList :submitValue="todoList" />
  </div> 
</template>

<script lang="ts">
import {Vue, Component } from 'vue-property-decorator';
import ItemList from './components/ItemList.vue';

  
//compontents:{}
@Component({
  components:{
    // ItemList:ItemList
    ItemList
  }
})
export default class App extends Vue {
  //data(){return{}}
  mydata : string = '';
  todoList: Array<{
    id: number,
    text: string,
    completed: boolean
  }> = [];




  //method
  addTodo(text: string){
 
    if(!text){
      alert('please input text');
      return
    }
     this.todoList.push({
      id: Date.now(),
      text,
      completed: false
    });
    localStorage.setItem('todoList',JSON.stringify(this.todoList));
    this.mydata = '';
  
    // console.log(this.mySubmit);
    
  }

}

</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}


</style>
