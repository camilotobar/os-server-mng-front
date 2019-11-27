<template>
    <v-app>
        <v-content>
            <Header @environmentChanged="environmentChanged" @killProcess="killProcess" :performance="performance"></Header>
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
            performance: null,
        }),
        mounted() {
            this.environmentChanged('Linux');
        },
        methods: {
            environmentChanged(environment) {
                this.currentEnvironment = environment;
                axios.get(`http://localhost:8080/performanceOn${environment}`).then((response) => {
                  this.performance = response.data;
                  this.processes = response.data.processes;
                });
            },
            killProcess(pid) {
                axios.get(`http://localhost:8080/killOn${this.currentEnvironment}?pid=${pid}`).then((response) => {
                  this.performance = response.data;
                  this.processes = response.data.processes;
                });
            },
        }
    };
</script>
