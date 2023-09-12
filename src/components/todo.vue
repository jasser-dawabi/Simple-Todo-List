<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue TodoApp</h2>

    <div class="d-flex">
      <input v-model="storage" type="text" placeholder="Enter Task" class="form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>

    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(tasks,index) in tasks" :key="index">
      <td>
        <span :class="{'finished': tasks.status === 'finished'}">
          {{ tasks.name }}
        </span>
      </td>
        <td>
          <span @click="changeStatus(index)" class="pointer" :class="{'text-danger':  tasks.status === 'to-do', 'text-warning':tasks.status === 'in-progress', 'text-success':tasks.status ==='finished'}">
            {{ tasks.status }}
          </span>
        </td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
  </tbody>
</table>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{

      storage: "",
      editedTasks: null,
      availableTasks:['to-do', 'in-progress', 'finished'],
      tasks: [
        {
          name: "Clean up room",
          status: "to-do"
        },
        
        {
          name: "Check Student Works",
          status: "finished"
        }
      ]
    }

  },

  methods: {
    submitTask(){
      if(this.storage.length ===0) return;
      
      if(this.editedTasks === null){
      this.tasks.push({
        name:this.storage,
        status: 'to-do'
      });
      }else{
        
        this.tasks[this.editedTasks].name=this.storage
        this.editedTasks = null;
      }
      this.storage='';
    },
    
    deleteTask(index){
      this.tasks.splice(index,1);
    },

    editTask(index){
      this.storage = this.tasks[index].name;
      this.editedTasks = index;
    },

    changeStatus(index){
      let newIndex = this.availableTasks.indexOf(this.tasks[index].status);
      if(++newIndex > 2) 
      newIndex = 0;
      this.tasks[index].status=this.availableTasks[newIndex];
    },

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
  cursor: pointer;
}

.finished{
  text-decoration: line-through;
}
</style>
