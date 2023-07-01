<template>
  <div class="app-container">
    <b-card v-if="!isMobile()" class="app-quote-card border-0 text-center">
      <b-row>
        Discover Delicious <mark class="magenta">Recipes</mark> at Your Fingertips!
      </b-row>
      <b-row class="d-flex w-100 justify-content-center">
        <img src="~/assets/chef.png" />
      </b-row>
    </b-card>
    <SearchCard :class="{ 'app-search-card': !isMobile(), 'app-search-card-mobile': isMobile() }" />
  </div>
</template>

<script>
import SearchCard from '../components/SearchCard.vue';
export default {
  name: 'IndexPage',
  components: {
    SearchCard
  }
}
</script>

<style>
body {
  box-sizing: border-box;
  font-family: 'Nunito', Arial, Helvetica, sans-serif;
  background: #eeebee url('~assets/background.png') left top / 400px 300px no-repeat;
}

.app-container {
  display: grid;
  grid-template-columns: 40% 60%;
  grid-template-rows: 60% 40%;
  min-height: 100vh;
}

.app-search-card {
  grid-column: 2;
  grid-row: 1/3;
  display: flex;
  align-self: center;
  margin: 0 auto;
  width: 90%;
  height: 90%;
}

.app-search-card-mobile {
  grid-column: 1/3;
  grid-row: 1/3;
  display: flex;
  align-self: center;
  margin: 0 auto;
  width: 90%;
  height: 90%;
}

.app-quote-card {
  grid-column: 1;
  grid-row: 2;
  display: flex;
  align-self: center;
  align-items: center;
  margin: 0 auto;
  width: 90%;
  height: 72%;
  background: #ffffff81;
  font-weight: 800;
  font-size: 1.2rem;
  color: #0d131c
}

.app-quote-card img {
  width: 50px;
  height: 50px;
  animation: tilt-shaking .5s infinite;
}

.magenta {
  color: #fe043d;
  background: none;
}

@keyframes tilt-shaking {
  0% {
    transform: rotate(0deg);
  }

  25% {
    transform: rotate(5deg);
  }

  50% {
    transform: rotate(0eg);
  }

  75% {
    transform: rotate(-5deg);
  }

  100% {
    transform: rotate(0deg);
  }
}
</style>