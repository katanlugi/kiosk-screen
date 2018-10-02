<template>
    <main>
        <!-- <carousel :perPageCustom="[[480, 2], [768, 3]]"> -->
        <carousel :perPage="1" :autoplay="true" :loop="true" :paginationEnabled="false" :autoplayTimeout="5000">
            <slide v-for="slide in this.slides" :key="slide.index">
                <!-- <span class="label" :class="`--${slide.index}`">{{slide.name}}</span> -->
                <!-- <img :src="slide.url" style="width: 300px; max-width: 100%;"> -->
                <img class="slide-img" :src="slide.url">
            </slide>
            
        </carousel>
    </main>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
export default {
    name: 'slider',
    components: {
        Carousel, Slide
    },
    data() {
        return {
            slides: [
                {
                    'index': 1,
                    'name': '1',
                    'url': 'http://www.labrioche-orvin.ch/wp-content/uploads/20140911_LABRIOCHE_1_0456-30rc4nywn23iaus8a5jrpm.jpg'
                },
                {
                    'index': 2,
                    'name': '2',
                    'url': 'http://www.labrioche-orvin.ch/wp-content/uploads/Croissants-30ll7ez0uixwnd537ls362.jpg'
                },
                {
                    'index': 3,
                    'name': '3',
                    'url': 'http://www.labrioche-orvin.ch/wp-content/uploads/Header3-2yo4fm6bzz4imduq2fy422.png'
                },
                {
                    'index': 4,
                    'name': '4',
                    'url': 'http://www.labrioche-orvin.ch/wp-content/uploads/BriocheChoco-30ll61udu4ja0ea7lwhpmy.jpg'
                },
            ]
        }
    },
}
</script>

<style lang="scss" >
.VueCarousel-inner {
    // transition: transform 137.333ms ease 0ms !important;
    transition: opacity 2.0s ease-in;
}

// .VueCarousel-slide {
//     opacity: 0 !important;
//     flex-basis: 0;
// }

// .VueCarousel-slide-active {
//     transition: all 0.5s !important;
//     opacity: 1 !important;
// }
.VueCarousel-slide {
    position: relative;
    background: darkslategrey;
    color: #fff;
    font-family: Arial;
    font-size: 24px;
    text-align: center;
    min-height: 100px;
    width: 100%;
}

.slide-img {
    width: 100%;
    object-fit: fill;
}

.label {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(177, 177, 177, 0.9);
    border: 1 solid black;
    z-index: 100;
}
// .slide {
//     background: {
//         position: center;
//         size: cover;
//     }
//     height: 500px;

//     &--1 {
//         // background-image: url(../img/bg-1_1.jpg);
//         background-image: url('http://www.labrioche-orvin.ch/wp-content/uploads/20140911_LABRIOCHE_1_0456-30rc4nywn23iaus8a5jrpm.jpg');
//     }
//     &--2 {
//         // background-image: url(../img/bg-1_1.jpg);
//         background-image: url('http://www.labrioche-orvin.ch/wp-content/uploads/Croissants-30ll7ez0uixwnd537ls362.jpg');
//     }
// }
</style>
