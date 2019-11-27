<template>
    <v-app>
        <v-content>
            <Header @environmentChanged="environmentChanged" @killProcess="killProcess"></Header>
        </v-content>
        <Processes :processes="processes"></Processes>
    </v-app>
</template>

<script>
    import axios from 'axios';
    import Header from "./components/Header";
    import Processes from "./components/Processes";

    export default {
        name: 'App',
        components: {
            Processes,
            Header
        },
        data: () => ({
            currentEnvironment: '',
            processes: [],
        }),
        mounted() {
            this.environmentChanged('Linux');
        },
        methods: {
            environmentChanged(environment) {
                this.currentEnvironment = environment;
                axios.get(`http://localhost:8080/performanceOn${environment}`).then((response) => {
                  let performance = response.data;
                  this.processes = performance.processes;
                });
            },
            killProcess(pid) {
                axios.get(`http://localhost:8080/killOn${this.currentEnvironment}?pid=${pid}`).then((response) => {
                  let performance = response.data;
                  this.processes = performance.processes;
                });
            },
        }
    };
</script>
