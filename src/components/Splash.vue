<template>
  <div>
    <h1>Social <span class="flicker">Nights</span></h1>
    <ul class="menu-container main-menu">
      <li class="join-header main-menu-item">
        Join a Room:
      </li>
      <li class="room-id">
        <input type="text" id="room-input" class="text-input" v-model="joinRoomID"
        placeholder="Room ID" @keyup.enter="joinRoom"/>
      </li>
      <li class="join-error">
        {{ roomError }}
      </li>
      <li class="or-header main-menu-item">
        Or
      </li>
      <li class="menu-item main-menu-item host-button" v-on:click="hostRoom">
        <form id="loginForm" action="http://localhost:8082/auth/spotify" method="GET">
          Host a Room
        </form>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Splash',

  data() {
    return {
      joinRoomID: '',
      roomError: '',
    };
  },

  mounted() {
    document.getElementById('room-input').focus();
  },

  methods: {
    hostRoom() {
      document.getElementById('loginForm').submit();
    },

    joinRoom() {
      this.roomError = '';

      if (this.joinRoomID.length !== 5) {
        this.roomError = 'Room must be 5 characters';
      }
      if (!/^[a-z0-9]+$/i.test(this.joinRoomID)) {
        this.roomError = 'Room ID only uses letters and numbers';
      }
      if (!this.joinRoomID) {
        this.roomError = 'Enter a room ID';
      }
      if (!this.roomError) {
        this.$router.push({ path: `/room/${this.joinRoomID}` });
      }
    },
  },
};
</script>

<style scoped>
h1 {
  margin: .3em;
  text-shadow: 0 0 1em #fff, 0 0 .4em #ff1493;
}

li {
  display: inline-block;
}

.flicker {
  animation: flicker 10s linear infinite;
}

@keyframes flicker {
  0%, 19.999%, 22%, 62.999%, 64%, 64.999%, 70%, 100% {
    opacity: 1;
    text-shadow: 0 0 1em #fff, 0 0 .4em #0ff;
  }
  20%, 21.999%, 63%, 63.999%, 65%, 69.999% {
    opacity: 0.4;
    text-shadow: none;
  }
}

.main-menu {
  margin: auto;
  width: 100%;
}

.main-menu-item {
  width: 80%;
  font-family: "Comfortaa";
  font-size: 1.5em;
  font-weight: 700;
  padding: 2.5vw 1.5vw;
  margin: 1vh 0;
}

.join-header {
  padding-bottom: 0;
}

.or-header {
  padding: 1vh;
  margin: 0;
}

.room-id {
  width: 100%;
}

.room-id > input {
  width: 80%;
  margin: 1vw 0;
}

.join-error {
  margin-top: 0;
  color: #900;
}

.host-button {
  margin-top: 0vh;
}

@media screen and (min-width: 900px) {
  .main-menu {
    width: 50%;
  }

  .main-menu-item {
    padding: 1.5vw;
  }

  .join-header {
    padding-bottom: 0;
  }
}
</style>
