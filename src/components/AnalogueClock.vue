<template>
    <div class="analogue-clock-a">
        <!-- <h1>Clock</h1> -->
        <div class="dial">
            <div class="dot"></div>
            <div class="sec-hand"></div>
            <div class="sec-hand shadow"></div>
            <div class="min-hand"></div>
            <div class="min-hand shadow"></div>
            <div class="hour-hand"></div>
            <div class="hour-hand shadow"></div>
            <span class="twelve">12</span>
            <span class="three">3</span>
            <span class="six">6</span>
            <span class="nine">9</span>
            
            <span class="diallines" 
                v-for="i in this.range(0, 59)" :key="`k-${i}`"
                :style="`transform: rotate(${i*6}deg);`">
            </span>
            
            <div class="date"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'analogue-clock',
    computed: {
        dialLines() {
            return document.getElementsByClassName('diallines');
        },
        secHand() {
            return document.getElementsByClassName('sec-hand');
        },
        minHand() {
            return document.getElementsByClassName('min-hand');
        },
        hourHand() {
            return document.getElementsByClassName('hour-hand');
        },
        day() {
            return document.getElementsByClassName('date');
        }
    },
    created() {

    },
    mounted() {
        this.$nextTick(function () {
            window.setInterval(() => {
                this.tick();
            },1000);
        });

        // setInterval(this.tick(), 100);
    },
    methods: {
        range(start, end) {
            return [...Array(1+end-start).keys()].map(v => start+v);
        },
        tick() {
            const date = new Date();
            const seconds = date.getSeconds();
            const minutes = date.getMinutes();
            const hours = date.getHours();
            const day = date.getDate();
            
            const secAngle = seconds * 6;
            const minAngle = minutes * 6 + seconds * (360/3600);
            const hourAngle = hours * 30 + minutes * (360/720);
            
            for (const el of this.secHand) {
                el.style.transform = `rotate(${secAngle}deg)`;
            }
            for (const el of this.minHand) {
                el.style.transform = `rotate(${minAngle}deg)`;
            }
            for (const el of this.hourHand) {
                el.style.transform = `rotate(${hourAngle}deg)`;
            }
            for (const el of this.day) {
                el.innerText = day;
            }
        }
    }
}
</script>

<style lang="scss">
.analogue-clock-a {
    transform: scale(0.8);
}
.dial {
    // flex-grow: 1;
    // position: absolute;
    // top: 0; left: 0;
    // height: 100%;
    // width: 100%; 
    position: relative;
    width: 350px;
    height: 350px;
    background: #ececec;
    border: 12px solid #5c5c5c;
    border-radius: 50%;
    margin: 8% auto 0;
    box-shadow: 1px 14px 21px 0 rgba(0,0,0,.2);
    
    // transform: scale(0.5);
}

span {
   display: inline-block;
}

.dot {
   position: absolute;
   top: 0;
   left: 0;
   right: 0;
   bottom: 0;
   margin: auto;
   width: 16px;
   height: 16px;
   border-radius: 50%;
   background: radial-gradient(ellipse 20px 15px at 50% 0, #ececec 40%, #5c5c5c 80%);
   z-index: 10;
   box-shadow: 0 2px 5px 0 rgba(0,0,0,.3);
}

.sec-hand {
   position: absolute;
   top: 39px;
   left: 50%;
   margin-left: -7px;
   width: 14px;
   height: 162px;
   background: url('https://themegion.github.com/AnalogClock/sec.svg') 50% 50% no-repeat;
   z-index: 9;
   transform-origin: 50% 136px;
}

.sec-hand.shadow {
   top: 46px;
   margin-left: -4px;
   background-image: url('https://themegion.github.com/AnalogClock/sec-shdw.svg');
   opacity: .1;
   z-index: 8;
   filter: blur(2px);
}

.min-hand {
   position: absolute;
   top: 51px;  
   left: 50%;
   margin-left: -8px;
   width: 16px;
   height: 144px;
   background: url('https://themegion.github.com/AnalogClock/min.svg') 50% 50% no-repeat;
   z-index: 7;
   transform-origin: 50% 124px;
}

.min-hand.shadow {
   top: 58px;
   margin-left: -5px;
   background-image: url('https://themegion.github.com/AnalogClock/min-shdw.svg');
   opacity: .1;
   z-index: 6;
   filter: blur(2px);
}

.hour-hand {
   position: absolute;
   top: 85px;
   left: 50%;
   margin-left: -7px;
   width: 14px;
   height: 110px;
   background: url('https://themegion.github.com/AnalogClock/hour.svg') 50% 50% no-repeat;
   z-index: 5;
   transform-origin: 50% 90px;
}

.hour-hand.shadow {
   top: 92px;
   margin-left: -4px;
   background-image: url('https://themegion.github.com/AnalogClock/hour-shdw.svg');
   opacity: .1;
   z-index: 4;
   filter: blur(2px);
}

.twelve,
.three,
.six,
.nine {
   position: absolute;
   font-family: Lato, sans-serif;
   font-size: 32px;
   color: #777;
}

.twelve {
   top: 35px;
   left: 155px;
}

.three {
   top: 156px;
   right: 39px;
}

.six {
   left: 165px;
   bottom: 35px;
}

.nine {
   top: 156px;
   left: 39px;
}

.diallines {
   position: absolute;
   top: 15px;
   left: 50%;
   margin-left: -1px;
   width: 2px;
   height: 10px;
   background: #b3b3b0;
   z-index: 1;
   transform-origin: 50% 160px;
}

.diallines:nth-of-type(5n) {
   position: absolute;
   top: 10px;
   left: 50%;
   margin-left: -2px;
   width: 4px;
   height: 25px;
   background: #b3b3b0;
   z-index: 1;
   transform-origin: 50% 165px;
}

.date {
   position: absolute;
   top: 242px;
   left: 50%;
   margin-left: -18px;
   width: 36px;
   height: 30px;
   background: #83837a;
   border-radius: 6px;
   font-family: 'Fjalla One', sans-serif;
   font-size: 21px;
   line-height: 30px;
   color: white;
   text-align: center;
   box-shadow: inset 0 2px 2px 0 rgba(0,0,0,.3), inset 0 -2px 2px 0 rgba(255,255,255,.2);
}
</style>
