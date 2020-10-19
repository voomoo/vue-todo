<template>
  <v-app>
    <v-container>
      <v-row align="start">
        <v-col cols="12" md="10" align-self="center">
          <v-text-field
            @keyup.enter="addTask()"
            v-model="newTask"
            prepend-inner-icon="mdi-briefcase-plus"
            solo
            label="Enter a task..."
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="2">
          <v-btn @click="addTask()" large color="green">Add a task</v-btn>
        </v-col>
      </v-row>
    </v-container>
    <v-container>
      <v-card
        v-for="(task, index) in tasks"
        :key="index"
        class="px-6 my-2 mr-4"
      >
        <v-row justify="space-around">
          <v-col cols="12" md="1" align-self="center">
            <v-icon :color="iconColor">mdi-briefcase</v-icon>
          </v-col>
          <v-col cols="12" md="7" align-self="center">
            <h4 class="grey--text text--lighten-4">{{ task }}</h4>
          </v-col>
          <v-col cols="12" md="2" align-self="center">
            <v-btn @click="done(index)" color="green">Done</v-btn>
          </v-col>
          <v-col cols="12" md="2" align-self="center">
            <v-btn @click="del(index)" color="red">Delete</v-btn>
          </v-col>
        </v-row>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
import { bus } from "../main.js";
export default {
  data() {
    return {
      tasks: [],
      newTask: "",
      iconColor: "white",
    };
  },
  methods: {
    addTask() {
      if (this.newTask.length > 0) {
        this.tasks.unshift(this.newTask);
      }
      this.newTask = "";

      console.log(this.tasks);
    },
    del(i) {
      this.tasks = this.tasks.filter((item, index) => index !== i);
    },
    done(i) {
      bus.$emit("completed", this.tasks[i]);
      this.tasks = this.tasks.filter((item, index) => index !== i);
    },
  },
};
</script>

<style>
</style>