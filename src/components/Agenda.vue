<template>
    <div>
        <div class="events">
            <div class="event" v-for="event in this.events" :key="event.id">
                <div class="my-date">
                    <div class="day">{{ getDay(event.date) }}</div>
                    <div class="month">{{ getMonth(event.date).toUpperCase() }}</div>
                </div>
                <div class="title">
                    <p>{{event.title}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import {format, parse} from 'date-fns';
import CalendarDate from '@/components/CalendarDate.vue';
const locales = {
    en: require('date-fns/locale/en'),
    fr: require('date-fns/locale/fr'),
    de: require('date-fns/locale/de')
}
export default {
    name: 'agenda',
    props: ['lang'],
    components: {
        CalendarDate,
    },
    computed: {
        selectedLocale() {
            switch (this.lang) {
                case 'fr':
                    return locales.fr;
                case 'de':
                    return locales.de;
                default:
                    return locales.en;
            }
        }
    },
    data() {
        return {
            events: [
                {
                    'id': 1,
                    'date': '2018-10-27',
                    'title': 'Match au loto'
                },
                {
                    'id': 2,
                    'date': '2018-11-23',
                    'title': 'Concerts du Chandor'
                },
                {
                    'id': 3,
                    'date': '2018-12-01',
                    'title': 'Match au loto – FC Orvin'
                },
            ]
        }
    },
    methods: {
        getMonth(date) {
            const parsed = parse(date, 'YYYY-MM-DD');
            const formated = format(parsed, 'MMM', {locale: this.selectedLocale});
            return formated;
        },
        getDay(date) {
            const parsed = parse(date, 'YYYY-MM-DD');
            const formated = format(parsed, 'D', {locale: this.selectedLocale});
            return formated;
        },
    }
}
</script>

<style lang="scss" scoped>
.events {
    display: grid;
    grid-gap: 15px;
    grid-template-columns: 1fr;
}
.event {
    padding: 10px 5px 10px 5px;
    box-shadow: 3px 4px 20px 0px rgba(0, 0, 0, 0.8);
    // border: 1px solid green;
    display: grid;
    grid-template-columns: 90px auto;
    .my-date {
        font-size: 150%;
        font-weight: bold;
        color: #f9d50f;
        // background-color: aqua;
    }
    .title {
        flex-direction: column;
        justify-content: center;
        font-weight: bold;
        font-size: 110%;
        // p {
        //     resize: vertical;
        //     overflow: auto;
        // }
    }
}

</style>
