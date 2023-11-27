<template>
    <div>
        <table class="app-info-table">
            <thead>
                <tr>
                    <th>Zone</th>
                    <th>Puls</th>
                    <th>Trainingsbereich</th>
                    <th>Belastung</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(zone, index) in Object.values(zones)" :key="index"
                    :style="{ backgroundColor: zoneColors[index] }">
                    <td>{{ 'Zone ' + (index + 1) }}</td>
                    <td>{{ `${zone.min} - ${zone.max}` }}</td>
                    <td>{{ zone.description }}</td>
                    <td>{{ getBelastungDescription(zone.description) }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'AppInfoTable',
    props: ['zones', 'maxBPM'],
    data() {
        return {
            zoneColors: ["#2269e5", "#04f759", "#fce302", "#fc9700", "#ed1e1e"]
        };
    },
    methods: {
        getBelastungDescription(description) {
            if (description === 'Regeneration') {
                return 'Sehr leichtes Training';
            } else if (description === 'Fettverbrennung') {
                return 'Leichtes Training';
            } else if (description === 'Aerobe Ausdauer') {
                return 'Mittleres Training';
            } else if (description === 'Anaerobe Ausdauer') {
                return 'Schweres Training';
            } else if (description === 'Maximale Leistung') {
                return 'Sehr schweres Training';
            } else {
                return '';
            }
        }
    }

}
</script>

<style scoped>
.app-info-table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
    border: 1px solid black;
    border-radius: 5px;
}

.app-info-table thead th {
    background-color: black;
    color: #fff;
    text-align: left;

}

.app-info-table th,
.app-info-table td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}

.app-info-table th {
    background-color: #f2f2f2;
}

.app-info-table tr:nth-child(even) {
    background-color: #f9f9f9;
}
</style>