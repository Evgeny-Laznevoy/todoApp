<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title
        class="flex text-center"
        v-text="`${name}'s To Do List`"
      ></v-toolbar-title>
      <!-- <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn> -->
    </v-app-bar>

    <v-main>
      <v-container>
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
        <v-row class="blue-grey">
          <v-col>
            <v-checkbox
              color="secondary"
              v-model="hideCompleted"
              :label="`Hide completed tasks`"
            ></v-checkbox>
          </v-col>
        </v-row>
      </v-container>
      <!-- <HelloWorld/> -->
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';

export default {
  name: "App",

  components: {
    // HelloWorld,
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
  },
  created() {
    let data = localStorage.getItem("todos")
    if (data != null) {
      this.tasks = JSON.parse(data)
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
