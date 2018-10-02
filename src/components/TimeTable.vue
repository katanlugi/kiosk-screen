<template>
    <div>
        <h2>📍 {{ this.station }}</h2>
        
        <div class="items">
            <div class="item" v-for="item in this.timetable" :key="item.name">
                <div class="time">{{ getTime(item.stop.departure) }}</div>
                <div class="destination">{{ item.to }}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            station: '[not set]',
            timetable: [],
            stationboard: [],
        }
    },
    mounted() {
        this.loadData();
    },
    methods: {
        loadData() {
            const location = 'Orvin, place du village';
            const limit = 5;
            const url = `http://transport.opendata.ch/v1/stationboard?station=${location}&limit=${limit}`
            fetch(url)
                .then(response => {
                    response.json().then(data => {
                        this.station = data.station.name;
                        this.timetable = data.stationboard;
                    });
                });
        },
        getTime(date) {
            const datetime = date.split('T')[1].split(':');
            const h = datetime[0];
            const m = datetime [1];
            const time = `${h}:${m}`;
            return time;
        }
    }
}
</script>

<style lang="scss" scoped>

.items {
    display: grid;
    grid-gap: 15px;
    grid-template-columns: 1fr;
}
.item {
    padding: 10px 5px 10px 5px;
    box-shadow: 3px 4px 20px 0px rgba(0, 0, 0, 0.8);
    // border: 1px solid green;
    display: grid;
    grid-template-columns: 90px auto;
    .time {
        font-size: 150%;
        font-weight: bold;
        color: #f9d50f;
    }
    .destination {
        font-weight: bold;
        font-size: 120%;
        flex-direction: column;
        justify-content: center;
    }
}


</style>
