<template>
  <v-app>
    <v-container>
      <v-card
        v-for="(task, index) in tasks"
        :key="index"
        class="px-6 my-2 mr-4"
      >
        <v-row justify="space-around">
          <v-col cols="12" md="1" align-self="center">
            <v-icon color="green">mdi-briefcase</v-icon>
          </v-col>
          <v-col cols="12" md="7" align-self="center">
            <h4 class="grey--text text--lighten-4">{{ task }}</h4>
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
import { bus } from "../main";
export default {
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
      del(i) {
          this.tasks = this.tasks.filter((item, index) => index !== i)
      }
  },
  created() {
    bus.$on("completed", (data) => {
      this.tasks.unshift(data);
    });
  },
};
</script>

<style>
</style>