<template>
    <MapKakao :latitude="37.39843974939604" :longitude="127.10972941510465" />
</template>

<script>
import MapKakao from '@/components/Mapkakao.vue';
export default {
    components: {
        MapKakao
    }
}
</script>