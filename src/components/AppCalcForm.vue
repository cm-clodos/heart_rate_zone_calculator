<template>
    <div>
        <h1 class="title">Berechne deine Herzfrequenz Trainingszonen</h1>
        <div class="input-container">
            <label class="input-label">Maximale Herzfrequenz</label>
            <input type="number" class="input-field" v-model="maxBPM" @keyup.enter="calcTrainingZones">
            <button type="button" class="calc-button" @click.prevent="calcTrainingZones">Berechne</button>
        </div>

    </div>
    <div>
        <app-chart :zones="zones" :maxBPM="maxBPM"></app-chart>
    </div>
    <div>
        <app-info-table :zones="zones"></app-info-table>
    </div>
</template>

<script>
import AppChart from './AppChart.vue';
import AppInfoTable from './AppInfoTable.vue';

export default {
    name: 'AppCalcForm',
    components: {
        AppChart,
        AppInfoTable

    },
    data() {
        return {
            maxBPM: 0,
            zones: {
                one: {
                    min: 0,
                    max: 0,
                    description: 'Regeneration'
                },
                two: {
                    min: 0,
                    max: 0,
                    description: 'Fettverbrennung'
                },
                three: {
                    min: 0,
                    max: 0,
                    description: 'Aerobe Ausdauer'
                },
                four: {
                    min: 0,
                    max: 0,
                    description: 'Anaerobe Ausdauer'
                },
                five: {
                    min: 0,
                    max: 0,
                    description: 'Maximale Leistung'
                }
            }

        }
    },
    methods: {
        calcTrainingZones() {
            this.zones.one.min = Math.round(this.maxBPM * 0.5);
            this.zones.one.max = Math.round(this.maxBPM * 0.6);
            this.zones.two.min = Math.round(this.maxBPM * 0.6);
            this.zones.two.max = Math.round(this.maxBPM * 0.7);
            this.zones.three.min = Math.round(this.maxBPM * 0.7);
            this.zones.three.max = Math.round(this.maxBPM * 0.8);
            this.zones.four.min = Math.round(this.maxBPM * 0.8);
            this.zones.four.max = Math.round(this.maxBPM * 0.9);
            this.zones.five.min = Math.round(this.maxBPM * 0.9);
            this.zones.five.max = Math.round(this.maxBPM * 1);
        }
    }
}
</script>

<style scoped>
.title {
    text-align: center;
    margin-bottom: 20px;
}

.input-container {
    text-align: center;
    margin-top: 20px;
    margin-bottom: 20px;
}

.input-label {
    font-weight: bold;
    margin-right: 10px;

}

.input-field {
    padding: 8px;
    margin-bottom: 10px;
    width: 200px;
    font-size: 16px;
}

.calc-button {
    padding: 8px 16px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    margin-left: 10px;
    transition: background-color 0.3s, transform 0.3s;
}

.calc-button:hover {
    background-color: #45a049;
    transform: scale(1.1);
}
</style>