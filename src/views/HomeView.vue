<template>
<div style="margin-top: 20vw;" id="likes-container">
  <div class="head">
    <img src="https://i.postimg.cc/52sSDZxK/IMG-2627.jpg" width="40px" style="margin-top: 15px; margin-left: 10px; border-radius: 15px;">
    <p id="username" style="color: white; font-family: Geologica; position: absolute; margin-top: -35px; margin-left: 60px;">@{{ user }}</p>
  </div>
  <div style="text-align: center; margin-top: 50px;">
      <span class="score" id="count"><b>{{ likeCount }}</b></span><br>
      <button class="like" id="like" @click="tap"><img class="tap" src="https://i.postimg.cc/Rh1cdYsR/724-EDD19-EB0-C-4368-9-C2-F-4938769-DF5-FD.png"></button>
  </div>
        <div class="bar">
          <RouterLink to="/task">
            <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px" style="position: absolute; margin-left: 50vw; margin-top: 1vw;">
               <button class="task">Task</button>
          </RouterLink>
          <RouterLink to="/leader">
            <img src="https://i.postimg.cc/pLFMzbNx/DC99-DC47-4-E36-454-D-ADAE-8-EBF88812855.png" width="55px" style="position: absolute; margin-left: 8vw;">
              <button class="game">Game</button>
          </RouterLink>
          <RouterLink to="/leader">
            <img src="https://i.postimg.cc/tCz2cBhP/D384540-F-C585-455-C-AAB5-D10-FA58774-B2.png" width="50px" style="position: absolute; margin-left: 12vw; margin-top: 3vw">
              <button class="soon">Leaders</button>
          </RouterLink>
        </div>
</div>
</template>

<style scoped>
  body {
      background-color: #1c1c1d;
      touch-action: none;
  }
  .score {
      font-family: Geologica;
      color: white;
      font-size: 36px;
  }
  .like {
      margin-top: 20%;
      background-color: #1c1c1d;
      border: none;
  }
  .tap:active {
      transform: translateY(5px);
  }
  .tap {
      width: 320px;
      background-color: #1c1c1d;
  }
  .bar {
      background-color: #2c2c2e;
      bottom: 0;
      width: 150%;
      height: 10%;
      border-radius: 25px;
      margin-left: -40vw;
      position: fixed;
  }
  .task {
      background-color: #2c2c2e;
      width: 33vw;
      height: 105px;
      border: none;
      font-family: Geologica;
      color: rgb(82, 82, 82);
      margin-left: 38vw;
  }
  .game {
      background-color: #2c2c2e;
      width: 33vw;
      height: 100px;
      border: none;
      font-family: Geologica;
      color: rgb(17, 117, 193);
      margin-left: -2vw;
  }
  .soon{
      background-color: #2c2c2e;
      width: 38vw;
      height: 105px;
      border: none;
      font-family: Geologica;
      color: rgb(82, 82, 82);
      margin-left: -1vw;
  }
  .head {
    background-color: #252525;
    margin-left: -2vw;
    width: 105%;
    margin-top: -20vw;
    height: 70px;
  }
</style>

<script setup>
import { ref, onMounted } from 'vue';
import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-app.js";
import { getDatabase, ref as dbRef, set, get, onValue } from "https://www.gstatic.com/firebasejs/11.0.1/firebase-database.js";

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
const likeCount = ref(0);
let username;

const getUser = () => {
    username = "username";
};

const tap = async () => {
  username = getUser();
  const countsRef = dbRef(db, `counts/${username}`);
  try {
    const snapshot = await get(countsRef);
    let tap = snapshot.exists() ? snapshot.val().count : 0;
    tap++;
    likeCount.value = tap;
    await set(countsRef, { count: tap });
  } catch (error) {
    console.error("Error updating taps:", error);
  }
};


const fetchInitialLikeCount = async () => {
  username = getUser();
  const countsRef = dbRef(db, `counts/${username}`);
  try {
    const snapshot = await get(countsRef);
    if (snapshot.exists()) {
      likeCount.value = snapshot.val().count;
    }
  } catch (error) {
    console.error("Error fetching initial taps count:", error);
  }
};
onMounted(fetchInitialLikeCount);
</script>

<script>
export default {
  data() {
     return {
         user: window.Telegram.WebApp.initDataUnsafe.user.username
      }
  }
}
</script>
