<template>
    <v-card class="pa-5 ma-10" outlined>
        <v-form>
            <v-row>
                <v-col>
                    <h1>Remove process</h1>
                    <div class="d-flex">
                        <v-text-field class="mr-7" label="Process ID (PID)" outlined></v-text-field>
                        <v-btn class="mr-7" @click="killProcess">Kill Process</v-btn>
                    </div>
                </v-col>
                <v-col>
                    <h1>Get Performance From</h1>
                    <v-select :items="environments" label="Environments" @change="environmentChanged" outlined></v-select>
                </v-col>
            </v-row>
            <v-row>
                <v-col>
                    <h2>Task Stats</h2>
                    <p>Number of Task: {{ performance.tasks }}</p>
                    <p>Task Running: {{ performance.tasksRunning }}</p>
                    <p>Task Sleeping: {{ performance.tasksSleeping }}</p>
                    <p>Task Stopped: {{ performance.tasksStopped }}</p>
                    <p>Task Zombies: {{ performance.tasksZombies }}</p>
                </v-col>
                <v-col>
                    <h2>Memory Stats</h2>
                    <p>Memory Total: {{ performance.memoryTotal }}</p>
                    <p>Memory Free: {{ performance.memoryFree }}</p>
                    <p>Memory Used: {{ performance.memoryUsed }}</p>
                    <p>Swap Total: {{ performance.swapTotal }}</p>
                    <p>Swap Free: {{ performance.swapFree }}</p>
                    <p>Swap Used: {{ performance.swapUsed }}</p>
                </v-col>
            </v-row>
        </v-form>
    </v-card>
</template>

<script>
    export default {
        name: "Header",
        props: {
            performance: Object,
        },
        data() {
            return {
                environments: [ 'Linux', 'Windows' ],
                pid: '',
                environmentChoosed: '',
            };
        },
        methods: {
            environmentChanged(){
                this.$emit('environmentChanged', this.environmentChoosed);
            },
            killProcess(){
                this.$emit('killProcess', this.pid);
            }
        }
    }
</script>

<style scoped>

</style>
