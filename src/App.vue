<template>
  <div class="container">
   <h2 class="text-center mt-5">Vue Todo App</h2>
  <div class="d-flex "><input v-model="task" type="text" placeholder="Enter Text Here" class="form-control">
  <button @click="submittask" type="button" class="btn btn-warning">Submit</button>
  </div>
  <table class="table table-bordered mt-5">
  <thead>
    <tr >
      <th scope="col">Task Name</th>
      <th scope="col">Task Status</th>
      <th scope="col">Edit</th>
      <th scope="col">Delete</th>
    </tr>
  </thead>
  <tbody>
   <tr v-for="(task,index) in tasks" :key="index">
      <td><span :class="{ 'finished': task.status === 'Finished' }">
              {{ task.name }}
            </span></td>
      <td><span @click="changeStatus(index)">{{task.status}}</span></td>
      <div class="text-center" @click="edittask(index)">
      <td> <span class='fa fa-pen'></span></td>
      </div>
      <td>
        <div class ="text-center" @click="deletetask(index)">
        <span class='fa fa-trash'></span>
        </div>
      </td>
    </tr>
   
  </tbody>
</table>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  Components: {
    HelloWorld
  },
  data(){
    return{
      task:'',
      editedtask:null,
      avilablestatuses:['To-Do','Finished','In-progress'],
      tasks:[
      {
        
      }
     
      ] 
     
    }
    },
    methods : {
      submittask(){
        if(this.task.length==0)return;

        if(this.editedtask===null){
        this.tasks.push({
          name:this.task,
          status:"Todo"
        })}else{
          this.tasks[this.editedtask].name = this.task;
          this.editedtask=null;
        }
         this.task='';

      },
     deletetask(index){
       this.tasks.splice(index,1);
      },
      edittask(index){
        this.task=this.tasks[index].name;
        this.editedtask= index;
      },
      changeStatus(index){
      let newIndex = this.avilablestatuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.avilablestatuses[newIndex];
      }
    }

  }


</script>
<style scoped>
.finished{
   text-decoration: line-through;
}
</style>