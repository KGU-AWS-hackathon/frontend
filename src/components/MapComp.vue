<template>
    <div>
        <input v-model="latitudeInput" placeholder="Latitude" />
        <input v-model="longitudeInput" placeholder="Longitude" />
        <button v-on:click="updateCoordinates">Update</button>
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
