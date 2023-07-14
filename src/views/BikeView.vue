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

    <div>
      <geo-location />
    </div>

    <div class="mt-5" v-for="station in filteredStations" :key="station.stationId" @click="showCoordinates(station)">
      <h3>{{ station.stationName }}</h3>
      <p class="mt-3">거치대 개수: {{ station.rackTotCnt }} 개</p>
      <p>대여 가능 수: {{ station.parkingBikeTotCnt }} 대</p>
      <p>자전거 거치율: {{ station.shared }}%</p>
      <p>위도: {{ station.stationLatitude }}</p>
      <p>경도: {{ station.stationLongitude }}</p>
    </div>

    <div class="d-flex justify-content-center my-3">
      <button class="btn" @click="previousPage" :disabled="currentPage === 1">
        이전
      </button>
      <button class="btn" @click="nextPage" :disabled="currentPage === totalPages">
        다음
      </button>
    </div>
  </div>
  
</template>

<script>
import MapComp from '@/components/MapComp.vue';
import axios from 'axios';
import GeoLocation from './GeoLocation.vue';

const apiKey = process.env.VUE_APP_API_KEY;

export default {
  data() {
    return {
      bikeStations: [],
      searchQuery: "",
      currentPage: 1,     // 현재 페이지 번호
      pageSize: 5,       // 한 페이지에 표시되는 스테이션 개수
    };
  },
  created() {
    axios
      .get(`http://openapi.seoul.go.kr:8088/${apiKey}/json/bikeList/1/1000/`)
      .then((response) => {
        this.bikeStations = response.data?.rentBikeStatus?.row;
      })
      .catch((error) => {
        console.error("자전거 대여 데이터를 가져오는 중 오류 발생:", error);
      });
  },
  computed: {
    filteredStations() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.bikeStations.slice(startIndex, endIndex).filter((station) => {
        const searchRegex = new RegExp(this.searchQuery, "i");
        return (
          searchRegex.test(station.stationName) ||
          searchRegex.test(station.stationLatitude) ||
          searchRegex.test(station.stationLongitude)
        );
      });
    },
    totalPages() {
      return Math.ceil(this.bikeStations.length / this.pageSize);
    },
  },
  methods: {
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    showCoordinates(station) {
      console.log("선택된 스테이션의 위도:", station.stationLatitude);
      console.log("선택된 스테이션의 경도:", station.stationLongitude);
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
  components: { MapComp, GeoLocation }
};
</script>
