<template>
    <div v-if="tick" class="clock-container">
        <analogue :minutes="time.minutes" :tick="tick" :decimal="false"></analogue>
    </div>
</template>

<script>
import Analogue from '@/components/Analogue.vue';
export default {
    name: 'clock',
    components: { Analogue },
    data() {
        return {
            tick: 0,
            time: { hours: 0, minutes: 0, seconds: 0 }
        }
    },
    methods: {
        updateTime(time) {
            this.tick++
            this.time = {
                hours: time.getHours(),
                minutes: time.getMinutes(),
                seconds: time.getSeconds()
            }

            setTimeout(() => this.updateTime(new Date()), 1000 - new Date().getMilliseconds())
        }
    },
    mounted() {
        this.updateTime(new Date())
    }
}
</script>

<style>
.clock-container {
    /* background-color: aliceblue; */
    /* border: 1px solid green; */
    /* color: blue; */
    /* background-color: azure; */
    
    transform: scale(1);
}
</style>
