<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title
        class="flex text-center"
        v-text="`${name}'s To Do List`"
      ></v-toolbar-title>
    </v-app-bar>
    
    <v-main>
      <v-container>
        <div v-if="filteredTasks.length == 0">
          <div class="text-center">
            <b>Nithing to do. Hurrah!</b>
          </div>
        </div>
        <template v-else>
          <v-row>
            <v-col class="font-weight-bold">Task</v-col>
            <v-col cols="2" class="font-weight-bold">Done</v-col>
          </v-row>
          <v-row v-for="task in filteredTasks" :key="task.action">
            <v-col>{{ task.action }}</v-col>
            <v-col cols="2">
              <v-checkbox
                v-model="task.done"
                :label="`${task.done}`"
              ></v-checkbox>
            </v-col>
          </v-row>
        </template>
        <v-row cols="12">
          <v-col cols="10">
            <v-text-field
              v-model="newItemText"
              label="New To Do"
              solo
              clearable
            ></v-text-field>
          </v-col>
          <v-col cols="2">
            <v-btn cols="2" large color="primary" @click="addNewToDo"
              >Add</v-btn
            >
          </v-col>
        </v-row>
        <v-row align="center" justify="center" class="flex blue-grey">
          <v-col>
            <v-checkbox
              color="secondary"
              v-model="hideCompleted"
              :label="`Hide completed tasks`"
            ></v-checkbox>
          </v-col>
          <v-col>
            <v-btn @click="deleteCompleted">
              Delete Completed
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: "App",

  components: {

  },

  data: () => ({
    name: "Evgen",
    hideCompleted: false,
    newItemText: "",
    tasks: [
      { action: "Buy Flowers", done: false },
      { action: "Get Shoes", done: false },
      { action: "Collect Tickets", done: true },
      { action: "Call Joe", done: false },
    ],
  }),
  computed: {
    filteredTasks() {
      return this.hideCompleted
        ? this.tasks.filter((t) => !t.done)
        : this.tasks;
    },
  },
  methods: {
    addNewToDo() {
      if (this.newItemText !== "") {
        this.tasks.push({
          action: this.newItemText,
          done: false,
        });
        localStorage.setItem("todos", JSON.stringify(this.tasks));
        this.newItemText = "";
      }
    },
    sorteData(){
      localStorage.setItem('todos', JSON.stringify(this.tasks))
    },
    deleteCompleted(){
      this.tasks = this.tasks.filter(t => !t.done)
      this.sorteData()
    }
  },
  created() {
    let data = localStorage.getItem("todos");
    if (data != null) {
      this.tasks = JSON.parse(data);
    }
  },
};
</script>

<style>
.v-input--selection-controls {
  margin-top: 0 !important;
  padding-top: 0 !important;
}
</style>
