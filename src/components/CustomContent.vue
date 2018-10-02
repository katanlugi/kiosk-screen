<template> 
    <div class="custom-content">
        <div class="panel wide-panel">
            <logo></logo>
        </div>
        <!-- <div class="panel">
            <analogue-clock></analogue-clock>
        </div> -->
        <!-- <div class="panel">
            <clock-2></clock-2>
        </div> -->
        <clock class="panel"></clock>
        
        <div class="panel tall-panel">
            <h1>Agenda</h1>
            <agenda lang="fr"></agenda>
        </div>
        <!-- <div class="panel">
            <h1>Panel D</h1>
            <code>De la place pour quelque chose en plus...</code>
        </div> -->
        <div class="panel tall-panel">
            <h1>Horaire 🚌</h1>
            <time-table></time-table>
        </div>
        <div class="panel">
            <h1>Météo</h1>
            <weather :location-id="7286756" display="basic"></weather>
            <!-- <weather :location-id="7286756" :details="true"></weather> -->
        </div>
        <div class="panel">
            <h1>Météo</h1>
            <weather :location-id="7286756" display="detail"></weather>
        </div>
        <div class="panel wide-panel">
            <h1>Prévisions</h1>
            <weather-forcast :location-id="7286756" display="detail"></weather-forcast>
        </div>
        <div class="panel">
            <h1>Date</h1>
            <calendar-date :date="this.today" lang="fr"></calendar-date>
        </div>
    </div>
</template>

<script>
// import Slider from '@/components/Slider.vue';
import Logo from '@/components/Logo.vue';
import Clock from '@/components/Clock.vue';
// import Clock2 from '@/components/Clock2.vue';
import Agenda from '@/components/Agenda.vue';
import Weather from '@/components/Weather.vue';
import TimeTable from '@/components/TimeTable.vue';
import CalendarDate from '@/components/CalendarDate.vue';
import WeatherForcast from '@/components/WeatherForcast.vue';
// import AnalogueClock from '@/components/AnalogueClock.vue';

export default {
    name: 'custom-content',
    components: {
        Clock, Agenda, Weather, CalendarDate, Logo, TimeTable, WeatherForcast
    },
    data() {
        return {
            today: new Date(),
        }
    }
}
</script>

<style lang="scss" scoped>
    // .header {
    //     background-image: url('http://www.labrioche-orvin.ch/wp-content/uploads/20140911_LABRIOCHE_1_0456-30rc4nywn23iaus8a5jrpm.jpg');
    //     background-size: cover;
    //     background-repeat: no-repeat;
    //     background-position: center center;
    // }
    .custom-content > * {
        // margin: 10px;
        background-color: #2b2e35;
        // color: antiquewhite;
        color: white;
        border-radius: 5px;
        // padding: 10px;
        // font-size: 150%;
        // border: 1px dashed #aaa;

        h2 {
            color: rgb(156, 166, 176)
        }
    }
    
    .custom-content {
        background-color: rgb(26, 29, 36);//#14171c;//blanchedalmond;
        // grid-gap: 5px;
        grid-gap: 10px;
        width: 100%;
        display: grid;
        margin: 0 auto;
        // grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
        grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
        grid-auto-rows: minmax(150px, auto);
    }
    .header {
        grid-column: 1 / -1;
        grid-row: 1;
    }
    .top {
        grid-row: 1;
    }
    .panel {
        // background-color: #2b2e35;
        // border: 1px dotted green;
        // margin-left: 5px;
        // margin-right: 5px;
        flex: 1 1 200px;
        overflow: hidden;
    }
    .two-by-two {
        grid-row-end: span 2;
        grid-column: 1 / 3;
    }
    .tall-panel {
        grid-row: span 2;
    }
    .extra-wide-panel {
        grid-column: span 3;
    }
    .wide-panel {
        grid-column: span 2;
    }
    .header {
        
        img {
            // background-color: lightgray;
            // filter: invert(100%);
            filter: grayscale(1) invert(1);
        }
    }
</style>
