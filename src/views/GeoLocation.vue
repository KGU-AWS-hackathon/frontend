<template>
    <div>
        <button @click="getLocation">현재 위치 가져오기</button>
        <p v-if="locationError">{{ locationError }}</p>
        <p v-if="location">{{ location }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            location: null,
            locationError: null
        };
    },
    methods: {
        getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    this.handleSuccess,
                    this.handleError
                );
            } else {
                this.locationError = "Geolocation이 지원되지 않는 브라우저입니다.";
            }
        },
        handleSuccess(position) {
            this.location = `위도: ${position.coords.latitude}, 경도: ${position.coords.longitude}`;
        },
        handleError(error) {
            this.locationError = `위치 정보를 가져오는 중 오류가 발생했습니다: ${error.message}`;
        }
    }
};
</script>
