<template>
    <div>
        <!-- 데이터를 표시할 요소 -->
        <p>{{ fetchedData }}</p>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            fetchedData: null
        };
    },
    created() {
        this.getData();
    },
    methods: {
        getData() {
            axios.get('http://phopho.shop/')
                .then(response => {
                    this.fetchedData = response.data.message;
                })
                .catch(error => {
                    console.error(error);
                });
        }
    }
};
</script>
