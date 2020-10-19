<template>
  <v-app>
    <v-app-bar app dark>
      <v-toolbar-title>{{ date }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <h5 @click="incompleteTab()" :class="inactive">Incomplete Tasks</h5>
      <h5 @click="completeTab()" :class="active">Complete Tasks</h5>
    </v-app-bar>
    <v-main>
      <keep-alive>
        <Incomplete v-if="!complete"></Incomplete>
        <Complete v-else></Complete>
      </keep-alive>
    </v-main>
  </v-app>
</template>

<script>
import Incomplete from "./components/Incomplete";
import Complete from "./components/Complete";
export default {
  name: "App",

  components: { Incomplete, Complete },

  data: () => ({
    complete: false,
    active: "mx-4 grey--text",
    inactive: ""
    //
  }),
  methods: {
    completeTab() {
      if (!this.complete) {
        this.complete = true;
        this.active = "mx-4"
        this.inactive = "grey--text"
      }
      console.log(this.complete);
    },
    incompleteTab() {
      if (this.complete) {
        this.complete = false;
        this.active = "mx-4 grey--text"
        this.inactive = ""
      }
      console.log(this.complete);
    },
  },
  computed: {
    date() {
      var day = new Date().toLocaleString("en-us", { weekday: "long" });
      var month = new Date().toLocaleString("en-us", { month: "long" });
      var date = new Date().getDate();

      return `${day}, ${month} ${date}`;
    },
  },
};
</script>
<style scoped>
h5:hover{
  cursor: pointer;
}
</style>
