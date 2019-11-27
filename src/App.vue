<template>
  <v-app>
    <v-content>
      <Header @environmentChanged="environmentChanged" @killProcess="killProcess" :performance="performance"></Header>
    </v-content>
    <Processes
      ref="pro"
      :processes="processes"
      :environment="currentEnvironment"
      @killProcess="killProcess"
    ></Processes>
  </v-app>
</template>

<script>
import axios from "axios";
import Header from "./components/Header";
import Processes from "./components/Processes";

export default {
  name: "App",
  components: {
    Processes,
    Header
  },
  data: () => ({
    currentEnvironment: localStorage.getItem("envir"),
    processes: [],
      performance: null,
  }),
  mounted() {
    this.environmentChanged("Linux");
  },
  methods: {
    environmentChanged(environment) {
      this.currentEnvironment = environment;
      localStorage.setItem("envir", environment);
      axios
        .get(`http://localhost:8080/performanceOn${environment}`)
        .then(response => {
          let performance = response.data;
          if (this.currentEnvironment === "Windows") {
            this.processes = performance.processeswin;
          } else {
            this.processes = performance.processes;
            this.performance = response.data;
          }
        });
    },
    killProcess(pid) {
      axios
        .get(
          `http://localhost:8080/killOn${this.currentEnvironment}?pid=${pid}`
        )
        .then(response => {
          let performance = response.data;
          if (this.currentEnvironment === "Windows") {
            this.processes = performance.processeswin;
          } else {
            this.processes = performance.processes;
              this.performance = response.data;
          }
        });
    }
  }
};
</script>

<style>
    h1, h2 {
        color: #004479 !important;
    }
</style>
