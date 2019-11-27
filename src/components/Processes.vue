<template>
  <v-content>
    <v-card class="pa-5 ma-10" outlined>
      <v-data-table :items="processes" :headers="headers">
        <template v-slot:item.action="{ item }">
            <v-icon medium @click="killProcess(item)">delete</v-icon>
          </template>
      </v-data-table>
    </v-card>
  </v-content>
</template>

<script>
export default {
  name: "Processes",
  props: {
    processes: Array,
    environment: String
  },
  data() {
    return {};
  },
  computed: {
    headers() {
      let headers = [
        { text: "PID", value: "pid" },
        { text: "User", value: "user" },
        { text: "PR", value: "pr" },
        { text: "NI", value: "ni" },
        { text: "VIRT", value: "virt" },
        { text: "RES", value: "res" },
        { text: "SHR", value: "shr" },
        { text: "S", value: "s" },
        { text: "cpuUsedPercentage", value: "cpuUsedPercentage" },
        { text: "memoryUsedPercentage", value: "memoryUsedPercentage" },
        { text: "time", value: "time" },
        { text: "command", value: "command" },
        { text: "actions", value: "action", sortable: false }
      ];
      if (
        this.environment !== null &&
        this.environment !== undefined &&
        this.environment === "Windows"
      ) {
        headers = [
          { text: "PID", value: "pid" },
          { text: "Name", value: "name" },
          { text: "Handles", value: "handles" },
          { text: "NPM", value: "npm" },
          { text: "PM", value: "pm" },
          { text: "WS", value: "ws" },
          { text: "VM", value: "vm" },
          { text: "SI", value: "si" },
          { text: "CPU", value: "cpu" },
          { text: "actions", value: "action", sortable: false }
        ];
      }
      return headers;
    }
  },
  methods: {
    killProcess(item){
      if(confirm("Do you really want to delete The process " + item.name + "?")){
        this.$emit('killProcess', item.pid);
      }
    }
  }
};
</script>

<style scoped>
</style>
