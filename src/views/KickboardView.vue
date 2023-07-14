<template>
  <div>
    <h1>킥보드</h1>
     <div class="container-fluid">
      <form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
      </form>
    </div>
      <div class="mt-5" v-for="item in data" :key="item.NO">
        <p>{{ item.SGG_NM }} {{ item.ADDR }}</p>
        <p>{{ item.DADDR }}</p>
        <p>거치대 개수: {{ item.STAND_SIZE }}</p>
      </div>
  </div>
</template>

<script>
import axios from 'axios';

const apiKey = process.env.VUE_APP_API_KEY;


export default {
  data() {
    return {
      data: [],
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(`http://openapi.seoul.go.kr:8088/${apiKey}/json/parkingKickboard/1/20/`)
        .then(response => {
          this.data = response.data.parkingKickboard.row;
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>
