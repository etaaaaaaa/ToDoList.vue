<template>
  <div class="container">
    <h1 class="main_header">My Vue ToDo List</h1>

    <div class="main_add-container">
      <input class="main_input main_input-add" 
             type="text" 
             placeholder="Type in task" 
             v-model="task" 
             ref="inputbar"
             @keyup.enter="addTask">
      <button class="main_btn main_btn-add" 
              type="button" 
              @click="addTask">
        <icon-add class="main_icon" />
      </button>
    </div>

    <input class="main_input main_input-search" 
           type="text" 
           v-model="search"
           placeholder="Search task"
           @blur="() => {search = ''}">

    
    <div v-for="(task, index) in filteredTasks" :key="index">
      <ListItem @taskDone="() => {task.status = 'done'}"
                @deleteTask="() => {tasks.splice(index, 1)}"
                @editTask="editTask(index)"
                :taskInfo="task" 
                :index="index"
                :class="[ task.status === 'done' ? 'task_done' : '' ]"  />
    </div>
  </div>
</template>

<script>
import ListItem from './Items/ListItem.vue'
import IconAdd from './Icons/IconAdd.vue'

export default {
  components: {
    ListItem,
    IconAdd,
  },

  data() {
    return {
      task: "",
      search: "",
      editedTask: null,
      // local database
      tasks: [
        {
          name: "Do homework",
          status: "todo",
        },
        {
          name: "Die",
          status: "todo",
        },
        {
          name: "meow",
          status: "todo",
        },
      ]
    }
  },
  methods: {
    show() {
      console.log(this.tasks)
    },
    addTask() {
      if (this.task.length === 0) return;

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task.charAt(0).toUpperCase() + this.task.slice(1),
          status: 'to-do',
        })
      }else{
        this.tasks[this.editedTask].name = this.task
        this.editedTask = null
      }

      this.task = ""
    },
    editTask(index) {
      this.$refs.inputbar.focus()
      this.task = this.tasks[index].name;
      this.editedTask = index
    }
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter((task) => {
        return task.name.toLowerCase().match(this.search.toLowerCase())
      })
    }
  },
}
</script>

<style scoped>
.container {
  background-color: #ffbf6f;
  padding: 1rem;
  max-width: 604px;
  max-height: 590px;
  margin: 0 auto;
  overflow-y: scroll;
  border-radius: 0.5rem;
}
.main_header {
  text-align: center;
  margin-bottom: 1rem;
}
.main_input {  
  height: 65px;
  padding: 8px;
  border-radius: 0.5rem;
}
.main_add-container {
  display: inline-block;
  /* vertical-align: middle; */
}
.main_input-add {
  width: 95px;
  border-radius: 0.5rem 0 0 0.5rem;
}
.main_input-search {
  margin-left: 1rem;
}
.main_icon {
  width: 32px;
  fill: #fb7b3f;
}
.main_btn {
  height: 65px;
  width: 65px;
  border-radius: 0 0.5rem 0.5rem 0;
  background-color: #ffffff;
  vertical-align: top;
}

</style>