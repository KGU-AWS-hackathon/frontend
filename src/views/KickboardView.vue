<template>
  <div class="mx-3">
    <div>
      <MapComp />
    </div>

    <div class="container-fluid">
      <form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" v-model="searchQuery">
      </form>
    </div>

    <!-- <div>
      <GeoLocation />
    </div> -->

    <div class="mt-5" v-for="item in filteredData" :key="item.id" @click="showCoordinates(item)">
      <h5>{{ item.id }}. {{ item.detail }}</h5>
      <p class="mt-3">거치가능: {{ item.holder }}</p>
      <p>거치대 수: {{ item.holdersize }}</p>
      
    </div>
  </div>
</template>

<script>
import MapComp from '@/components/MapComp.vue';
import axios from 'axios';
// import GeoLocation from './GeoLocation.vue';

export default {
  data() {
    return {
      items: [], // 데이터를 저장할 배열명을 'items'로 변경
      searchQuery: '',
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
    showCoordinates(item) {
      console.log("선택된 스테이션의 위도:", item.ylocation);
      console.log("선택된 스테이션의 경도:", item.xlocation);

      localStorage.setItem("selectedLatitude", item.ylocation);
      localStorage.setItem("selectedLongitude", item.xlocation);

      location.reload();
    },
  },
  computed: {
    filteredData() {
      if (!this.searchQuery) {
        return this.items; // 'data'를 'items'로 변경
      }

      const searchRegex = new RegExp(this.searchQuery, 'i');

      return this.items.filter(item => {
        return (
          searchRegex.test(item.ylocation) || // 'SGG_NM', 'ADDR', 'DADDR'를 'ylocation', 'xlocation', 'holder', 'holdersize'로 변경
          searchRegex.test(item.xlocation) ||
          searchRegex.test(item.holder) ||
          searchRegex.test(item.holdersize)
        );
      });
    },
  },
  components: { MapComp }
};
</script>
