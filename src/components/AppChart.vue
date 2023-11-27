<template>
    <Bar :data="chartData" :options="chartOptions"></Bar>
</template>

<script>
import {
    Chart as ChartJS,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
    BarElement,

} from 'chart.js'
import { Bar } from 'vue-chartjs'
import ChartDataLabels from 'chartjs-plugin-datalabels';



ChartJS.register(
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
    BarElement,
    ChartDataLabels
)


export default {
    name: 'AppChart',
    components: {
        /* eslint-disable */
        Bar
        /* eslint-enable */
    },
    props: ['zones', 'maxBPM'],
    computed: {
        chartData() {
            return {
                labels: ['Zone 1', 'Zone 2', 'Zone 3', 'Zone 4', 'Zone 5'],
                datasets: [
                    {
                        label: 'Training Zones',
                        backgroundColor: ["#2269e5", "#04f759", "#fce302", "#fc9700", "#ed1e1e"],
                        borderWidth: 1,
                        borderColor: '#000',
                        data:
                            [
                                [this.zones.one.min, this.zones.one.max],
                                [this.zones.two.min, this.zones.two.max],
                                [this.zones.three.min, this.zones.three.max],
                                [this.zones.four.min, this.zones.four.max],
                                [this.zones.five.min, this.zones.five.max]
                            ]
                    }
                ]

            }
        },
        chartOptions() {
            return {
                responsive: true,
                indexAxis: 'y', // Set the index axis to 'x' for vertical bars and y for horizontal bars
                scales: {
                    x: {
                        display: true,
                        title: {
                            display: false,
                            text: 'BPM',
                            color: '#000',
                            font: {
                                size: 20,
                                lineHeight: 1.2,
                            },
                            padding: { top: 30, left: 0, right: 0, bottom: 0 }
                        },
                        beginAtZero: false,
                        ticks: {
                            font: 20,
                        },

                    },
                    y: {
                        display: true,
                        title: {
                            display: false,
                            text: 'Zones',
                            color: '#000',
                            font: {
                                size: 20,
                                lineHeight: 1.2,
                            },
                            padding: { top: 0, left: 0, right: 0, bottom: 30 }
                        },
                        beginAtZero: false,
                    }
                },
                plugins: {
                    datalabels: {
                        anchor: 'center',
                        align: 'center',
                        color: '#000',
                        font: {
                            size: 16,
                        },
                        formatter: function (value) {
                            return value.join(' - ') + ' BPM';
                        },
                    },


                },


            }

        },

    }
}
</script>

<style scoped></style>