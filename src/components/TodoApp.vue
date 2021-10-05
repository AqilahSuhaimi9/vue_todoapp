<template>
  <div class="container" style="max-width: 600px">
    <!--Heading-->
    <h2 class="text-center mt-5">My Vue Todo-list App</h2>
    
    <!--input for the app-->
    <div class="d-flex mt-5">
      <input v-model="task" type="text" placeholder="Enter task" class="w-100 form-control">
      <button class="btn btn-warning rounded-0" @click="submitTask"> SUBMIT </button>
    </div>

    <!--Table task part = will use from bootstrap-->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <!--Rename the header table-->
          <th scope="col">Task</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <!--using array + loop-->
          <!--npm install --save-dev @fortawesome/fontawesome-free-->
          <td>{{task.name}}</td>
          <!--Edit task section +icon-->
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <!--Delete task section + icon-->
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

  data() {
    return {
      task: '',
      editedTask: null,
      tasks: [
        {
          name: 'Meeting with team',
        },
        {
          name: 'Submit report',
        },
        {
          name: 'Eat lunch',
        }
      ],

    };
  },
  methods: {
    submitTask(){
      if(this.task.length === 0) return;
//to create new task or edit task
      if(this.editedTask == null){
        this.tasks.push({
          name: this.task,
        });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = '';
    },
    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
}



</style>
