<template>
  <div style="margin-top: 20vw;" id="likes-container">
    <div class="head">
      <img
        src="https://i.postimg.cc/52sSDZxK/IMG-2627.jpg"
        width="40px"
        style="margin-top: 15px; margin-left: 10px; border-radius: 15px;"
      />
      <p id="username" style="color: white; font-family: Geologica; position: absolute; margin-top: -35px; margin-left: 60px;">
        @{{ user }}
      </p>
    </div>
    <div style="text-align: center; margin-top: 30px;">
      <span class="score" id="count"><b>{{ likeCount }}</b></span><br />
      <div class="coin-container">
        <button class="like" id="like" @click="tap">
          <img
            class="tap"
            :class="{ shake: isShaking }"
            src="https://i.postimg.cc/Rh1cdYsR/724-EDD19-EB0-C-4368-9-C2-F-4938769-DF5-FD.png"
          />
        </button>
        <transition name="fade">
          <span v-if="showPlusOne" class="plus-one">+1</span>
        </transition>
        <transition name="fade">
          <div v-if="showFastTapMessage" class="chat-bubble">
            Tap-Tap!
          </div>
        </transition>
      </div>
    </div>

    <!-- Нижняя панель навигации -->
    <div class="bar">
      <RouterLink to="/task" class="nav-item" :class="{ 'game-active': $route.path === '/task' }">
        <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px">
        <button class="task"></button>
      </RouterLink>
      <RouterLink to="/" class="nav-item" :class="{ 'game-active': $route.path === '/' }">
        <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px">
        <button class="game"></button>
      </RouterLink>
      <RouterLink to="/leader" class="nav-item" :class="{ 'game-active': $route.path === '/leader' }">
        <img src="https://i.postimg.cc/5082bz0d/icons8-leaderboard-80.png" width="50px">
        <button class="soon"></button>
      </RouterLink>
    </div>
  </div>
</template>

<style scoped>
/* Остальные стили остаются без изменений */

/* Стили для нижней панели */
.bar {
  background-color: #2c2c2e;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 45px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  border-top-left-radius: 30px; /* Округление слева */
  border-top-right-radius: 30px; /* Округление справа */
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.2);
}

/* Стили для подсветки активной иконки */
.bar .nav-item.game-active img {
  filter: brightness(0) saturate(100%) invert(25%) sepia(90%) saturate(2000%) hue-rotate(220deg) brightness(90%) contrast(90%); /* Темно-синий цвет */
}

/* Расположение иконок */
.bar .nav-item {
  flex: 1; /* Равномерное распределение пространства */
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Смещение первой и последней иконки */
.bar .nav-item:first-child {
  margin-left: 10px; /* Смещение первой иконки влево */
}

.bar .nav-item:last-child {
  margin-right: 10px; /* Смещение последней иконки вправо */
}
</style>

<script setup>
import { ref, onMounted } from 'vue';
import { initializeApp } from 'https://www.gstatic.com/firebasejs/11.0.1/firebase-app.js';
import { getDatabase, ref as dbRef, set, get } from 'https://www.gstatic.com/firebasejs/11.0.1/firebase-database.js';

const firebaseConfig = {
  apiKey: 'AIzaSyBhTL7JcmGtdwPpJyKkwMRoIEOIU17ZxUk',
  authDomain: 'tapalka-c9556.firebaseapp.com',
  databaseURL: 'https://tapalka-c9556-default-rtdb.firebaseio.com',
  projectId: 'tapalka-c9556',
  storageBucket: 'tapalka-c9556.firebasestorage.app',
  messagingSenderId: '386428968826',
  appId: '1:386428968826:web:de56837a0bbc2cf27940c3',
  measurementId: 'G-YENX5XCT8J',
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const likeCount = ref(0);
const isShaking = ref(false);
const showPlusOne = ref(false);
const showFastTapMessage = ref(false);
const lastTapTime = ref(0);

const getUser = () => {
  return window.Telegram.WebApp.initDataUnsafe.user.username;
};

const tap = async () => {
  const username = getUser();
  const countsRef = dbRef(db, `counts/${username}`);
  try {
    const snapshot = await get(countsRef);
    let tap = snapshot.exists() ? snapshot.val().count : 0;
    tap++;
    likeCount.value = tap;
    await set(countsRef, { count: tap });

    isShaking.value = true;
    showPlusOne.value = true;

    setTimeout(() => {
      isShaking.value = false;
    }, 200);

    setTimeout(() => {
      showPlusOne.value = false;
    }, 800);

    const currentTime = Date.now();
    if (currentTime - lastTapTime.value < 300) {
      showFastTapMessage.value = true;
      setTimeout(() => {
        showFastTapMessage.value = false;
      }, 2000);
    }
    lastTapTime.value = currentTime;
  } catch (error) {
    console.error('Error updating taps:', error);
  }
};

const fetchInitialLikeCount = async () => {
  const username = getUser();
  const countsRef = dbRef(db, `counts/${username}`);
  try {
    const snapshot = await get(countsRef);
    if (snapshot.exists()) {
      likeCount.value = snapshot.val().count;
    }
  } catch (error) {
    console.error('Error fetching initial taps count:', error);
  }
};

onMounted(() => {
  fetchInitialLikeCount();
});
</script>

<script>
export default {
  data() {
    return {
      user: window.Telegram.WebApp.initDataUnsafe.user.username,
    };
  },
};
</script>
