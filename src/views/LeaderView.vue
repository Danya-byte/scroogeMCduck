<template>
  <center>
    <img src="https://em-content.zobj.net/source/telegram/386/trophy_1f3c6.webp" width="300vw" style="margin-top: 8vw">
  </center>
  <h2>Leaders:</h2>
  <div class="leader-container">
    <div class="lider" id="leaderboard">
      <table>
        <thead>
          <tr>
            <th style="font-family: Geologica;">User</th>
            <th style="font-family: Geologica;">Score</th>
          </tr>
        </thead>
        <tbody id="leaderboard-body">
          <tr v-for="(user, index) in sortedCounts" :key="index">
            <td>{{ user[0] }}</td>
            <td>{{ user[1].count }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <div class="bar">
    <RouterLink to="/task" class="nav-item">
      <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px" style="position: absolute; margin-left: 50vw; margin-top: 1vw">
      <button class="task"></button>
    </RouterLink>
    <RouterLink to="/" class="nav-item">
      <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px" style="position: absolute; margin-left: 8vw;">
      <button class="game"></button>
    </RouterLink>
    <RouterLink to="/leader" class="nav-item leader-active">
      <img src="https://i.postimg.cc/fRPzxjgn/0-F65-F8-E0-D77-D-464-C-B669-07-F0287-ABD7-C.png" width="50px" style="position: absolute; margin-left: 12vw; margin-top: 3vw">
      <button class="soon"></button>
    </RouterLink>
  </div>
</template>

<style scoped>
body {
  font-family: Geologica;
  color: white;
  touch-action: none;
  overflow-y: scroll;
}

.leader-container {
  height: 50vh; /* Задайте высоту контейнера, чтобы он занимал 50% высоты экрана */
  overflow-y: scroll; /* Включите вертикальную прокрутку */
  margin-top: 10vw;
  padding-bottom: 100px; /* Добавьте отступ снизу, чтобы контент не перекрывался с нижней панелью */
}

#leaderboard {
  width: 100%;
  text-align: center;
  color: white;
}

#leaderboard table {
  width: 100%;
  border-collapse: collapse;
  color: white;
}

#leaderboard th, #leaderboard td {
  padding: 10px;
  border: 1px solid #1c1c1d;
  text-align: left;
  color: white;
  font-family: Geologica;
}

h2 {
  margin-top: -5vw;
  position: absolute;
  color: white;
  font-family: Geologica;
}

.bar {
  background-color: #2c2c2e;
  bottom: 0;
  width: 150%;
  height: 9%;
  border-radius: 25px;
  margin-left: -40vw;
  position: fixed;
  overflow: hidden;
}

.task, .game, .soon {
  background-color: #2c2c2e;
  border: none;
  font-family: Geologica;
  color: white;
}

.task {
  width: 33vw;
  height: 105px;
  margin-left: 38vw;
  color: rgb(82, 82, 82);
}

.game {
  width: 33vw;
  height: 100px;
  margin-left: -2vw;
  color: rgb(82, 82, 82);
}

.soon {
  width: 38vw;
  height: 105px;
  margin-left: -1vw;
  color: rgb(17, 117, 193);
}

/* Стили для активного состояния */
.bar .nav-item.leader-active img {
  filter: brightness(0) saturate(100%) invert(25%) sepia(90%) saturate(2000%) hue-rotate(220deg) brightness(90%) contrast(90%); /* Темно-синий цвет */
}
</style>

<script>
import { initializeApp } from "firebase/app";
import { getDatabase, ref, onValue } from "firebase/database";

const firebaseConfig = {
  apiKey: "AIzaSyBhTL7JcmGtdwPpJyKkwMRoIEOIU17ZxUk",
  authDomain: "tapalka-c9556.firebaseapp.com",
  databaseURL: "https://tapalka-c9556-default-rtdb.firebaseio.com",
  projectId: "tapalka-c9556",
  storageBucket: "tapalka-c9556.firebasestorage.app",
  messagingSenderId: "386428968826",
  appId: "1:386428968826:web:de56837a0bbc2cf27940c3",
  measurementId: "G-YENX5XCT8J"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

export default {
  data() {
    return {
      counts: {}
    };
  },
  computed: {
    sortedCounts() {
      return Object.entries(this.counts).sort((a, b) => b[1].count - a[1].count);
    }
  },
  mounted() {
    const countsRef = ref(db, 'counts/');
    onValue(countsRef, (snapshot) => {
      this.counts = snapshot.val() || {};
    });
  }
};
</script>
