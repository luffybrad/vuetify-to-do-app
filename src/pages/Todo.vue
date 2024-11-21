<template>
    <div class="todo">


      <v-text-field
            v-model="newTaskTitle"
            @click:append-inner="addTask()"
            @keyup.enter = "addTask()"
            class="pa-3"
            append-inner-icon="mdi-plus"
            label="Add task"
            variant="underlined"
            hide-details
            clearable
          ></v-text-field>

  
    <v-list
      lines="one"
      select-strategy="leaf"
      class="pt-0"
      v-for="task in filteredTasks"
    >
      <v-list-item
        :key="task.id"
        :title="task.title"
        :value="task.done"

        @click="doneTask(task.id)"
        
        :class="{ 
          'bg-green-lighten-3' : task.done,
        }"
        
      >
        <template v-slot:prepend >
          <v-list-item-action>
            <v-checkbox-btn :model-value="task.done" color="success"></v-checkbox-btn>
          </v-list-item-action>
        </template>
        <template v-slot:append>
          <v-btn
          v-if="!task.done"
          @click.stop="deleteTask(task.id)"
            color="red lighten-1"
            icon="mdi-delete"
            variant="text"
          ></v-btn>
          <v-icon
          v-else
          color="success"
          >
          mdi-check
          </v-icon>
        </template>
      </v-list-item>
      <v-divider></v-divider>
    </v-list>

    </div>
  </template>

<script>

export default {
  data() {
      return{
    newTaskTitle: '',
    tasks: [
      { id: 1, title: 'Eat' , done: false},
      { id: 2, title: 'Sleep' , done: false},
      { id: 3, title: 'Code', done: false},
    ],
  }
},
props: {
  searchQuery : ""
},
computed: {
  filteredTasks(){
    if (!this.searchQuery){
      return this.tasks;
    }
    const lowerCaseQuery = this.searchQuery.toLowerCase();
    return this.tasks.filter(task => task.title.toLowerCase().includes(lowerCaseQuery))
  }
},
  methods: {
    addTask(){
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false
      }
      this.tasks.push(newTask)
      this.newTaskTitle=""
    },
    doneTask(id){
      let task = this.tasks.filter(task => task.id == id)[0]
      task.done = !task.done
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    handleSearchQuery(query){
      console.log("Searching for: ",query )
      this.tasks = this.tasks.filter(task => task.title == query)
    }
  },
  watch: {
    searchQuery(newQuery){
      console.log(newQuery)
    }
  }
}
</script>