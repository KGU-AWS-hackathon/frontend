<template>
    <div class="container">
        <div class="input-row">
            <input class="input-field" v-model="latitudeInput" placeholder="위도" />
            <input class="input-field" v-model="longitudeInput" placeholder="경도" />
        </div>
        <button class="update-button" v-on:click="updateCoordinates">검색</button>
        <MapKakao :latitude="latitude" :longitude="longitude" :key="mapKey" />
    </div>
</template>

<script>
import MapKakao from '@/components/Mapkakao.vue';

export default {
    components: {
        MapKakao,
    },
    data() {
        return {
            latitudeInput: '',
            longitudeInput: '',
            latitude: 37.55564880, // Default value
            longitude: 126.91062927, // Default value
            mapKey: 0, // Key for forcing map reload
        };
    },
    created() {
        const storedLatitude = localStorage.getItem("selectedLatitude");
        const storedLongitude = localStorage.getItem("selectedLongitude");

        if (storedLatitude && storedLongitude) {
            this.latitudeInput = storedLatitude;
            this.longitudeInput = storedLongitude;
        }
    },
    methods: {
        updateCoordinates() {
            this.latitude = parseFloat(this.latitudeInput);
            this.longitude = parseFloat(this.longitudeInput);
            this.mapKey += 1; // Increment key to force map reload
            console.log('입력한 위도:', this.latitude);
            console.log('입력한 경도:', this.longitude);
        },
        reloadMap() {
            this.mapKey += 1; // Increment key to force map reload
        },
        showCoordinates(station) {
            this.latitudeInput = station.stationLatitude;
            this.longitudeInput = station.stationLongitude;
        },
    },
    watch: {
        latitude() {
            this.reloadMap();
        },
        longitude() {
            this.reloadMap();
        },
    },
};
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.input-row {
    display: flex;
    margin-block: 10px;
}

.input-field {
    margin-bottom: 10px;
    margin-inline: 5px;
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.update-button {
    padding: 10px 20px;
    margin-bottom: 20px;
    background-color: #91c450;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
     width: 100%; /* 추가된 스타일 */
    box-sizing: border-box; /* 추가된 스타일 */
}
</style>