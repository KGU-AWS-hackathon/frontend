<template>
    <div class="container">
        <input class="input-field" v-model="latitudeInput" placeholder="Latitude" />
        <input class="input-field" v-model="longitudeInput" placeholder="Longitude" />
        <button class="update-button" v-on:click="updateCoordinates">Update</button>
        <MapKakao :latitude="latitude" :longitude="longitude" :key="mapKey" />
    </div>
</template>

<script>
import MapKakao from '@/components/Mapkakao.vue';

export default {
    components: {
        MapKakao
    },
    data() {
        return {
            latitudeInput: '',
            longitudeInput: '',
            latitude: 37.55564880, // Default value
            longitude: 126.91062927, // Default value
            mapKey: 0 // Key for forcing map reload
        };
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
        }
    },
    watch: {
        latitude() {
            this.reloadMap();
        },
        longitude() {
            this.reloadMap();
        }
    }
}
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.input-field {
    margin-bottom: 10px;
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.update-button {
    padding: 10px 20px;
    margin-bottom: 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
</style>