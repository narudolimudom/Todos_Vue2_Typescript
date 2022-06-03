<template>
  <div> 
      <div v-for="item in TempList" :key="item.id" class="item">
          <Item @delete ="deleteById" :todo="item" />   
      </div>
      <div class="filter-box">
            <span>{{countActive()}}</span> 
            <v-btn-toggle
          v-model="toggleExclusive"
          mandatory
        >
          <v-btn>
            <p>All</p>
          </v-btn>
          <v-btn>
            <p>Active</p>
          </v-btn>
          <v-btn>
            <p>Completed</p>
          </v-btn>
        </v-btn-toggle>
        <button v-if="checkClearStatus()" @click="romoveById()">Clear completed</button>
      </div>
    <!-- {{submitValue}} -->

    <!-- <p v-for="item in submitValue" :key="Date.now()+item">fast item</p> -->
  </div>
</template>

<script lang="ts">
import {Vue, Component, Prop, Watch } from 'vue-property-decorator';
import Item from './Item.vue';

@Component({
    components:{
        Item
    },

   
})
export default class ItemList extends Vue {

    //state 
    toggleExclusive : Number = 0;
    isNotClear : boolean = false;
    numberOfCompleted : number = 0;
    TempList : Array<{
        id: number,
        text: string,
        completed: boolean
    }> = [];



    mounted(){
        this.TempList = this.submitValue;
        // this.TempList = JSON.parse(localStorage.getItem('todoList') || '[]');
        
    }



    //watch
    @Watch('toggleExclusive')
    onToggleExclusive(val: number){
        if(val ==0){
            this.TempList = this.submitValue;
        }else if(val == 1){
            this.TempList = this.submitValue;
            this.TempList = this.TempList.filter(item => !item.completed);
        }else if(val == 2){
            this.TempList = this.submitValue;
            this.TempList = this.TempList.filter(item => item.completed);
        }
    }
    //check completed

    getDeleteId(id: string){
        this.numberOfCompleted++;
    }

    checkClearStatus(){
        this.numberOfCompleted = this.submitValue.filter(item => item.completed).length;
        if(this.numberOfCompleted !=0){
            return true;
        }else{
            return false;
        }
    }
    deleteById(id: number){
        //pop value from array
        this.submitValue.splice(this.submitValue.findIndex(item => item.id === id),1);
    }
    romoveById(){

        const   wantDelete = (this.submitValue.filter(item => item.completed));
        for(let i =0; i<wantDelete.length; i++){
            this.submitValue.splice(this.submitValue.findIndex(item => item.id === wantDelete[i].id),1);
        }
        
         
         
    

        // const numOfCompleted = this.submitValue.findIndex(item => item.completed);
        // console.log(numOfCompleted);
        
    }
    


    //props:{}
   @Prop({type:Array  ,default : ()=>[] })
   submitValue!: Array<{
    id: number,
    text: string,
    completed: boolean
  }>

  //methods:{}
    countActive(){
        const result = this.submitValue.filter(item => !item.completed).length;
        if(result %2  == 0){
            return result + " items left";
        }else{
            return result + " item left";
        }
    }


}

</script>

<style scoped>
.filter-box{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ccc;
    background-color: antiquewhite;
}

</style>