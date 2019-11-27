<template>
    <v-content>
        <v-card class="pa-5 ma-10" outlined>
            <v-data-table :items="processes" :headers="headers"></v-data-table>
        </v-card>
    </v-content>
</template>

<script>
    export default {
        name: "Processes",
        props: {
            processes: Array,
        },
        data() {
            return {
                headers: [
                    { text: 'PID', value: 'pid' },
                    { text: 'User', value: 'user' },
                    { text: 'PR', value: 'pr' },
                    { text: 'NI', value: 'ni' },
                    { text: 'VIRT', value: 'virt' },
                    { text: 'RES', value: 'res' },
                    { text: 'SHR', value: 'shr' },
                    { text: 'S', value: 's' },
                    { text: 'cpuUsedPercentage', value: 'cpuUsedPercentage' },
                    { text: 'memoryUsedPercentage', value: 'memoryUsedPercentage' },
                    { text: 'time', value: 'time' },
                    { text: 'command', value: 'command' },
                ],
            };
        },
    }
</script>

<style scoped>

</style>
