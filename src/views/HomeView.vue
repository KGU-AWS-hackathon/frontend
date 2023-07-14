<template>
  <div class="home">
    <!-- <h1>홈화면입니다</h1> -->
    <router-link to="/bike">
      <img class="image" alt="bike" src="@/assets/bike.jpg">
    </router-link>
    <router-link to="/kick">
      <img class="image" alt="kick" src="@/assets/kick.jpg">
    </router-link>
  </div>
</template>

<style>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.image {
  max-width: 100%;
  height: auto;
  /* margin-bottom: 10px; */
}
</style>
