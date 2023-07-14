<template>
    <div>
        <div v-for="item in items" :key="item.id">
            ID: {{ item.id }}<br>
            위도: {{ item.ylocation }}<br>
            경도: {{ item.xlocation }}<br>
            Holder: {{ item.holder }}<br>
            거치대 수: {{ item.holdersize }}
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            items: [],
        };
    },
    mounted() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            axios
                .get('http://phopho.shop/kickboard')
                .then(response => {
                    this.items = response.data;
                })
                .catch(error => {
                    console.log(error);
                });
        },
    },
};
</script>
