<template>
    <div>
        <!-- 데이터를 표시할 요소 -->
        <p>{{ fetchedData.isSuccess }}</p>
        <p>{{ fetchedData.code }}</p>
        <p>{{ fetchedData.message }}</p>
    </div>
<!-- 
    <button class="btn btn-primary btn-space" @click="frmLoginPopup.show(true)">
        Log In
    </button> -->
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            fetchedData: null,
            // frmLoginPopup: {},
        };
    },
    created() {
        this.getData();
    },
    methods: {
        getData() {
            axios.get('http://phopho.shop/')
                .then(response => {
                    this.fetchedData = response.data;
                })
                .catch(error => {
                    console.error(error);
                });
        }
    }
};
</script>
