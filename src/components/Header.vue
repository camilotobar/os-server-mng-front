<template>
    <v-card class="pa-5 ma-10" outlined>
        <v-form>
            <v-row>
                <v-col class="d-flex align-center" cols="5">
                    <div>
                        <h2>Select Environment To Get Performance</h2>
                        <v-select
                                :items="environments"
                                @change="environmentChanged"
                                label="Environments"
                                outlined
                                v-model="environmentChoosed"
                        ></v-select>
                    </div>
                </v-col>
                <v-col class="d-flex align-center justify-center" cols="3">
                    <v-flex class="text-xs-center">
                        <v-btn @click="environmentChanged" large>Refresh Table</v-btn>
                    </v-flex>
                </v-col>
                <v-col class="d-flex align-center" cols="4">
                    <v-flex class="text-xs-center">
                        <h1>Estudiantes</h1>
                        <p>Julián Tauta - Camilo Tobar</p>
                    </v-flex>
                </v-col>
            </v-row>
            <div v-if="performanceValid">
                <v-divider class="my-5 mx-3"></v-divider>
                <v-row>
                    <v-col>
                        <h2>Task Stats</h2>
                        <p><b>Number of Task:</b> {{ performance.tasks }}</p>
                        <p><b>Task Running:</b> {{ performance.tasksRunning }} | <b>Task Sleeping:</b> {{ performance.tasksSleeping }}</p>
                        <p><b>Task Stopped:</b> {{ performance.tasksStopped }} | <b>Task Zombies:</b> {{ performance.tasksZombies }}</p>
                    </v-col>
                    <v-col>
                        <h2>Memory Stats</h2>
                        <p><b>Memory Total:</b> {{ performance.memoryTotal }} | <b>Swap Total:</b> {{ performance.swapTotal }}</p>
                        <p><b>Memory Free:</b> {{ performance.memoryFree }} | <b>Swap Free:</b> {{ performance.swapFree }}</p>
                        <p><b>Memory Used:</b> {{ performance.memoryUsed }} | <b>Swap Used:</b> {{ performance.swapUsed }}</p>
                    </v-col>
                </v-row>
            </div>
        </v-form>
    </v-card>
</template>

<script>
    export default {
        name: "Header",
        props: {
            performance: Object
        },
        data() {
            return {
                environments: ["Linux", "Windows"],
                pid: "",
                environmentChoosed: ""
            };
        },
        computed: {
            performanceValid() {
                return this.performance !== undefined && this.performance !== null && this.environmentChoosed === "Linux"
            }
        },
        methods: {
            environmentChanged() {
                this.$emit("environmentChanged", this.environmentChoosed);
            },
            killProcess() {
                this.$emit("killProcess", this.pid);
            }

        }
    };
</script>

<style scoped>
</style>
