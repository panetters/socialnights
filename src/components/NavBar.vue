<template>
  <div>
    <ul class="menu-container navbar">
      <li class="menu-item topbar-item home" @click="leaveRoom">
        <img src="../assets/home.svg">
      </li>
      <li class="topbar-item logo">
        S<span class="logo-blue">N</span>
      </li>
      <li class="topbar-item username" v-if="getUsername">
        {{ getUsername }}
      </li>
    </ul>
    <div class="navbar-empty-div"></div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  name: 'NavBar',
  computed: mapGetters(['getUsername']),
  methods: mapActions(['leaveRoom']),
};
</script>

<style scoped>
.navbar {
  background: #333;
  position: fixed;
  width: 100%;
  z-index: 1000;
}

.navbar-empty-div {
  height: calc(5vh + 6vw);
  margin: 0;
  padding: 0;
}

.topbar-item {
  float: left;
  height: 5vh;
  padding: 0;
  margin: 3vw;
}

.home {
  width: 5vh;
  background: #333;
  border-radius: 50%;
  position: relative;
}

.home > img {
  height: 4vh;
  width: 4vh;
  position: absolute;
  top: calc(50% - 2vh);
  left: calc(50% - 2vh);
}

.logo {
  position: absolute;
  width: 15vw;
  left: calc(50% - 7.5vw);
  right: calc(50% - 7.5vw);
  line-height: 5vh;
  padding: 0;
  margin: 3vw 0;
  font-size: 2.5em;
  font-family: "Monoton";
  color: #ff1493;
}

.logo-blue {
  color: #0ff;
}

.username {
  font-family: "Comfortaa";
  float: right;
  font-size: 1.5em;
  padding: 0;
  line-height: 5vh;
  background: transparent;
}

@media screen and (min-width: 900px) {
  .navbar {
    background: transparent;
  }
  .topbar-item {
    height: 8vh;
    margin: 1vh;
  }

  .home {
    width: 8vh;
  }

  .username {
    line-height: 8vh;
    margin-right: 3vh;
  }

  .logo {
    font-size: 0em;
  }

  .home > img {
    height: 6vh;
    width: 6vh;
    top: calc(50% - 3.5vh);
    left: calc(50% - 3vh);
  }
}
</style>
