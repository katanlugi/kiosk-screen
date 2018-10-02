<template>
    <!-- <time :datetime="format(this.date, 'YYYY-MM-dd')" class="icon"> -->
    <time :datetime="this.datetime" class="icon">
        <em>{{this.dayString}}</em>
        <!-- <strong>September</strong> -->
        <strong>{{this.monthString}}</strong>
        <span>{{this.dayNumber}}</span>
    </time>
</template>

<script>
import {format} from 'date-fns';
const locales = {
  en: require('date-fns/locale/en'),
  fr: require('date-fns/locale/fr'),
  de: require('date-fns/locale/de')
}
export default {
    props: ['year', 'month', 'day', 'date', 'lang'],
    computed: {
        localDate() {
            if (this.date) {
                return this.date;
            } else {
                return new Date(this.year, this.month, this.day);
            }
        },
        datetime() {
            if (this.year && this.month && this.day) {
                return `${this.year}-${this.month}-${this.day}`;
            } else {
                return format(Date(Date.now()), 'YYYY-MM-D');
            }
        },
        monthString() {
            return format(new Date(this.localDate), 'MMMM', {locale: this.selectedLocale});
        },
        dayString() {
            return format(new Date(this.localDate), 'dddd', {locale: this.selectedLocale});
        },
        dayNumber() {
            return format(new Date(this.localDate), 'D');
        },
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
    created() {
        if (this.date) {
            console.log('date given', this.date);
        } else {
            console.log('year, month, day given', this.year, this.month, this.day);
        }

    }
}
</script>

<style scoped>
time {
    margin: 0 auto;
    padding: 0;
}
time.icon {
    font-size: 1em; /* change icon size */
    display: block;
    position: relative;
    width: 7em;
    height: 7em;
    background-color: #fff;
    border-radius: 0.6em;
    box-shadow: 0 1px 0 #bdbdbd, 0 2px 0 #fff, 0 3px 0 #bdbdbd, 0 4px 0 #fff, 0 5px 0 #bdbdbd, 0 0 0 1px #bdbdbd;
    overflow: hidden;
}
time.icon *
{
  display: block;
  width: 100%;
  font-size: 1em;
  font-weight: bold;
  font-style: normal;
  text-align: center;
}
time.icon strong
{
  position: absolute;
  top: 0;
  padding: 0.4em 0;
  color: #fff;
  background-color: #fd9f1b;
  border-bottom: 1px dashed #f37302;
  box-shadow: 0 2px 0 #fd9f1b;
}
time.icon em
{
  position: absolute;
  bottom: 0.3em;
  color: #fd9f1b;
}
time.icon span
{
  font-size: 2.8em;
  letter-spacing: -0.05em;
  padding-top: 0.8em;
  color: #2f2f2f;
}
</style>
