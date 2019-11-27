<template>
  <v-card class="pa-5 ma-10" outlined>
    <v-form>
      <v-row>
        <v-col>
          <h1>Select Environment To Get Performance</h1>
          <v-select
            v-model="environmentChoosed"
            :items="environments"
            label="Environments"
            @change="environmentChanged"
            outlined
          ></v-select>
        </v-col>
        <v-col>
          <v-flex class="text-xs-center">
            <h1 style="color:white">Hola</h1>
            <v-btn large @click="environmentChanged">Refresh Table</v-btn>
          </v-flex>
        </v-col>
      </v-row>
    </v-form>
  </v-card>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      environments: ["Linux", "Windows"],
      pid: "",
      environmentChoosed: ""
    };
  },
  methods: {
    environmentChanged() {
      this.$emit("environmentChanged", this.environmentChoosed);
    }
  }
};
</script>

<style scoped>
</style>
