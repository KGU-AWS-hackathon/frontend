<template>
  <div>
    <h1>Bike Rental Stations</h1>
    <input type="text" v-model="searchQuery" placeholder="검색어를 입력하세요" />
    <ul>
      <tr v-for="station in filteredStations" :key="station.stationId">
        <h3>{{ station.stationName }}</h3>
        <p>거치대 개수: {{ station.rackTotCnt }}</p>
        <p>대여 가능 수: {{ station.parkingBikeTotCnt }} 대</p>
        <p>자전거 거치율: {{ station.shared }}%</p>
        <p>위도: {{ station.stationLatitude }}</p>
        <p>경도: {{ station.stationLongitude }}</p>
      </tr>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

const apiKey = process.env.VUE_APP_API_KEY;

export default {
  data() {
    return {
      bikeStations: [],
      searchQuery: '',
    };
  },
  created() {
    axios
      .get(`http://openapi.seoul.go.kr:8088/${apiKey}/json/bikeList/1/1000/`)
      .then((response) => {
        this.bikeStations = response.data?.rentBikeStatus?.row;
      })
      .catch((error) => {
        console.error('Error retrieving bike rental data:', error);
      });
  },
  computed: {
    filteredStations() {
      return this.bikeStations.filter((station) => {
        const searchRegex = new RegExp(this.searchQuery, 'i');
        return (
          searchRegex.test(station.stationName) ||
          searchRegex.test(station.stationLatitude) ||
          searchRegex.test(station.stationLongitude)
        );
      });
    },
  },
};
</script>
