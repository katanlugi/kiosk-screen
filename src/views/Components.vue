<template>
    <div class="components">
        <h1>List of all components</h1>
        <h1>List of all components</h1>
        
        <clock></clock>
        <calendar-date :date="this.today" lang="fr"></calendar-date>
        <!-- <analogue-clock class="analogue-clock"></analogue-clock> -->
        <!-- <clock-2></clock-2> -->
    </div>
</template>

<script>
import Clock from '@/components/Clock.vue';
import Clock2 from '@/components/Clock2.vue';
import CalendarDate from '@/components/CalendarDate.vue';
import AnalogueClock from '@/components/AnalogueClock.vue';

export default {
    name: 'components',
    components: {
        Clock, CalendarDate, AnalogueClock, Clock2
    },
    data() {
        return {
            today: new Date(),
        }
    }
}
</script>

<style lang="scss" scoped>
.components > * {
    // margin: 10px;
    background-color: aliceblue;//#2b2e35;
    // color: antiquewhite;
    color: darkslategray;//white;
    border-radius: 5px;
    // padding: 10px;
    // font-size: 150%;
    // border: 1px dashed #aaa;

    h2 {
        color: rgb(156, 166, 176)
    }
}

.components {
    background-color: lightblue;//rgb(26, 29, 36);//#14171c;//blanchedalmond;
    grid-gap: 5px;
    width: 100%;
    display: grid;
    // margin: 0 auto;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    grid-auto-rows: minmax(150px, auto);
}
.analogue-clock {
    border: 1px solid green;
    transform: scale(0.5);
}
</style>
