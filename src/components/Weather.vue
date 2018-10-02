<template>
    <div class="weather">
        <!-- <img class="icon" :src="iconUrl" :alt="this.alt"> -->
        <div class="basic" v-if="this.display === 'basic'">
            <div class="icon">
                <img :src="iconUrl" :alt="this.alt">
            </div>
            <div class="temp">🌡 {{ this.currentTemp }}° C</div>
        </div>
        
        <!-- <div class="description">{{ this.currentdescription }}</div> -->
        
        <div class="details" v-if="this.display === 'detail'">
            <div class="icon">
                <img :src="iconUrl" :alt="this.alt">
            </div>
            <div class="temp">🌡 {{ this.currentTemp }}° C</div>
            <div class="detail">
                <header>Détails:</header>
                <!-- <div>Wind	{{ this.currentWindSpeed}} m/s</div>
                <div>Humidity:	{{this.currentHumididy}} %</div>
                <div>Precip: {{ this.currentPrecip }}</div>
                <div>Pressure	{{this.currentPressure}} hPa</div> -->
                <div>Wind</div>
                <div>{{ this.currentWindSpeed}} m/s</div>
                <div>Humidity</div>
                <div>{{this.currentHumididy}} %</div>
                <div>Precip</div>
                <div>{{ this.currentPrecip }}</div>
                <div>Pressure</div>
                <div>{{this.currentPressure}} hPa</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'weather',
    props: ['locationId', 'details', 'display',],
    data() {
        return {
            weather: null
        }
    },
    computed: {
        iconUrl() {
            if (this.weather) {
                return `http://openweathermap.org/img/w/${this.weather.weather[0].icon}.png`;
            } else {
                return '#';
            }
        },
        alt() {
            return (this.weather) ? this.weather.weather[0].description : '⏳';
        },
        currentTemp() {
            return (this.weather) ? (this.weather.main.temp - 274,15) : '⏳';
        },
        currentdescription() {
            return (this.weather) ? this.weather.weather[0].description : '⏳';
        },
        currentPressure() {
            return (this.weather) ? (this.weather.main.pressure) : '⏳';
        },
        currentPrecip() {
            return (this.weather) ? (this.weather.main.precipitaion) : '';
        },
        currentHumididy() {
            return (this.weather) ? (this.weather.main.humidity) : '';
        },
        currentWindSpeed() {
            return (this.weather) ? (this.weather.wind.speed) : '';
        }
    },
    created() {
        if (!this.locationId) {
            console.error('No locationId provided!');
        } else {
            this.loadweather();
        }
    },
    methods: {
        loadweather() {
            // const locationId = '7286756';
            const apiKey = '9e9275614ed8af845a98263dbd071626';
            const url = `http://api.openweathermap.org/data/2.5/weather?id=${this.locationId}&APPID=${apiKey}`
            fetch(url)
                .then(response => {
                    response.json().then(data => {
                        console.warn(data);
                        this.weather = data
                    });
                });
        }
    }
}
</script>

<style lang="scss" scoped>
.weather {
    display: grid;
    // grid-gap: 20px;
    grid-template-columns: 1fr;
}
.details {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: 1fr 1fr;
    justify-content: left;
    align-items: center;
    
    .temp {
        grid-row: 2;
        grid-column: 1;
    }
    .detail {
        text-align: left;
        grid-row-start: 1;
        grid-row-end: 2;
        grid-row: 1 / span 2;
        display: grid;
        grid-template-columns: 1fr 1fr;
        header {
            font-size: 120%;
            font-weight: bold;
            border-bottom: 2px solid #f9d50f;
            margin-bottom: 15px;
            grid-column: 1 / span 2;
        }
        div {
            font-size: 110%;
        }
    }
}
.icon {
    grid-row: 1;
    grid-column: 1;
    transform: scale(2);
}
.description {
    font-size: 150%;
}
.temp {
    color: #f9d50f;
    font-weight: bold;
    font-size: 200%;
}
.details {
    .icon {
        grid-row: 1;
        grid-column: 1;
    }
    
}
</style>
