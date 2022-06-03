<template>
  <div>
      <div class=" todo-box">
      <v-checkbox  :style="{'--is-completed': todo.completed ? 'line-through' : 'none'}" v-model="todo.completed" :label="todo.text"/>
    <v-icon @click="deleteTodo()" aria-hidden="false">mdi-close</v-icon>    
     </div>
     <v-divider></v-divider>
  </div>
</template>

<script lang="ts">

import {Vue, Component, Prop,Watch} from 'vue-property-decorator';

@Component
export default class Item extends Vue {

    //state
    // checkbox : boolean = false;
    countClear : number = 0;

    // @Watch('countClear')
    // onCountClear(val: number){
    //     this.$emit('isComplete', val);
    // }

    // ! sign =  cannot null or undefined
     @Prop({type:Object ,default() {return{}}}) todo!: {
    id: number,
    text: string,
    completed: boolean
  }

    deleteTodo(){
        this.$emit('delete',this.todo.id);
        //check completed
    }

}
</script>

<style scoped>
.todo-box{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

.addb{
    border: red solid 2px;
}
/deep/ .v-input .v-label {
    text-decoration: var(--is-completed);
}
</style>




