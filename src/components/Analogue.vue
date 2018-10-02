<template>
    <figure class="analogue-clock">
        <figcaption class="analog-clock__face">
            <span v-for="n in 60"
                :key="n"
                class="analog-clock__notch"
                :class="{ '-long': !(n % 5), '-xlong': !(n % 15) }"
                :style="{ transform: `rotate(${n * 6}deg)` }">
            </span>
            <span class="twelve" v-if="this.decimal">12</span>
            <span class="three" v-if="this.decimal">3</span>
            <span class="six" v-if="this.decimal">6</span>
            <span class="nine" v-if="this.decimal">9</span>
        </figcaption>

        <span class="analog-clock__hand -seconds" :style="seconds"></span>
        <span class="analog-clock__hand -minutes" :style="minutes"></span>
        <span class="analog-clock__hand -hours" :style="hours"></span>
    </figure>
</template>

<script>
export default {
    name: 'analogue',
    props: { minute: Number, tick: Number, decimal: Boolean },
    data() {
        return {
            rotation: { hours: 0, minutes: 0, seconds: 0 }
        }
    },
    computed: {
        hours() {
            return { transform: `translate3d(-50%, 0, 0) rotate(${this.rotation.hours}deg)` }
        },
        minutes() {
            return { transform: `translate3d(-50%, 0, 0) rotate(${this.rotation.minutes}deg)` }
        },
        seconds() {
            return { transform: `translate3d(-50%, 0, 0) rotate(${this.rotation.seconds}deg)` }
        }
    },
    watch: {
        tick() {
            this.rotation.seconds += 6
            this.rotation.minutes += 0.1
        },
        minute(to, from) {
            if (from === to) return;
            this.rotation.hours += 0.5
        }
    },
    mounted() {
        let date = new Date()
        let [h, m, s] = [date.getHours(), date.getMinutes(), date.getSeconds()]
        this.rotation = {
            hours: (h * 30) + (m * 0.5),
            minutes: (m * 6) + (s * 0.1),
            seconds: s * 6
        }
    }
}
</script>

<style lang="scss" scoped>

// light:
// $backgroundColor: white;
// $faceColor: aliceblue;
// $secondHansColor: darkorange;
// $notchColor: #a1adb3;
// $decimalColor: #676f74;

// dark blue:
// $backgroundColor: darkblue;
// $faceColor: rgb(5, 39, 68);
// $secondHansColor: rgb(238, 255, 0);
// $notchColor: #a2d9f3;
// $decimalColor: #94ddff;

// dark grey:
$backgroundColor: #666;
$faceColor: #2b2e35;
$secondHansColor: #f9d50f;
$notchColor: white;
$decimalColor: #bac6cc;

figure {
    height: 100%;
}
.analog-clock {
    span {
        display: inline-block;
    }
    top: 50%;
    right: 50%;
    width: 50vh;
    height: 50vh;
    width: 100px;
    height: 100px;
    position: absolute;
    border-radius: 100%;
    transform: translate3d(-1.5rem, -50%, 0);
    filter: drop-shadow(0 0.125rem 0.5rem rgba(black, 0.1));

    &::after {
        top: 50%;
        left: 50%;
        content: '';
        width: 2.5%;
        height: 2.5%;
        position: absolute;
        border-radius: 100%;
        background-color: #edbec5;
        transform: translate3d(-50%, -50%, 0);
    }

    &__face {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        
        background-color: $faceColor;
    }

    &__notch {
        transform-origin: 50% 100%;
        position: absolute;
        width: 2px;
        height: 48%;
        bottom: 50%;
        left: 49%;

        &::after {
            content: '';
            width: 100%;
            height: 4%;//2.5%;
            position: absolute;
            top: 0;
            left: 0;
            background-color: $notchColor;//#b6c3c9;
        }

        &.-long::after {
            width: 4px;//2px;
            height: 10%;//7.5%;
        }
        &.-xlong::after {
            width: 6px;//2px;
            height: 13%;//7.5%;
        }
    }

    &__hand {
        transform-origin: 50% 100%;
        background-color: #7392a0;
        position: absolute;
        width: 4px;
        height: 40%;
        bottom: 50%;
        left: 50%;
        border-radius: 2px;
        transition: transform 1s linear;

        &::after {
            content: '';
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            height: 10%;
            background-color: inherit;
            backface-visibility: hidden;
        }

        &.-hours {
            height: calc(100% / 3);
            width: 6px;
            border-radius: 3px;
            transition: transform 60s linear;
        }

        &.-seconds {
            width: 2px;
            height: 45%;
            border-radius: 0;
            background-color: $secondHansColor;//darkorange;// #edbec5;
            transition: transform 100ms cubic-bezier(.6, .05, 0, 1.6);

            &::after {
                height: 12.5%;
            }
        }
    }
}
.twelve,
.three,
.six,
.nine {
    position: absolute;
    font-family: Lato, sans-serif;
    font-size: 32px;
    color: $decimalColor;
}

.twelve {
    top: 10%;
    left: 44%;
}

.three {
    top: 44%;
    right: 19%;
}

.six {
    left: 46.5%;
    bottom: 10%;
}

.nine {
    top: 44%;
    left: 17%;
}
</style>
