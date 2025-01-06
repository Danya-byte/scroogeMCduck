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
      <!-- Контейнер для монетки и анимации +1 -->
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
        <!-- Облачко с сообщением -->
        <transition name="fade">
          <div v-if="showFastTapMessage" class="chat-bubble">
            Tap-Tap!
          </div>
        </transition>
      </div>
    </div>

    <!-- Нижняя панель навигации -->
    <div class="bar">
      <RouterLink to="/task" class="nav-item" :class="{ active: $route.path === '/task' }">
        <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px" />
        <button class="task"></button>
      </RouterLink>
      <RouterLink to="/" class="nav-item" :class="{ active: $route.path === '/' }">
        <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px" />
        <button class="game"></button>
      </RouterLink>
      <RouterLink to="/leader" class="nav-item" :class="{ active: $route.path === '/leader' }">
        <img src="https://i.postimg.cc/fRPzxjgn/0-F65-F8-E0-D77-D-464-C-B669-07-F0287-ABD7-C.png" width="50px" />
        <button class="soon"></button>
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
.tap {
  width: 250px; /* Уменьшили размер монетки */
  background-color: #1c1c1d;
  transition: transform 0.1s ease-in-out;
}
.tap:active {
  transform: translateY(5px);
}
.head {
  background-color: #252525;
  margin-left: -2vw;
  width: 105%;
  margin-top: -20vw;
  height: 70px;
}

/* Контейнер для монетки и анимации +1 */
.coin-container {
  position: relative;
  display: inline-block;
  margin-top: 20px; /* Подняли монетку выше */
}

/* Анимация тряски монетки */
.shake {
  animation: shake 0.2s ease-in-out;
}

@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-5px);
  }
  50% {
    transform: translateX(5px);
  }
  75% {
    transform: translateX(-5px);
  }
}

/* Анимация +1 */
.plus-one {
  position: absolute;
  top: -30px; /* Позиция над монеткой */
  left: 50%;
  transform: translateX(-50%);
  font-family: Geologica;
  font-size: 36px; /* Увеличили размер шрифта */
  color: #ffd700; /* Золотой цвет */
  animation: floatUp 0.8s ease-in-out;
  font-weight: bold; /* Делаем текст жирным */
  text-shadow: 0 0 10px rgba(255, 215, 0, 0.8); /* Добавляем тень для эффекта свечения */
}

@keyframes floatUp {
  0% {
    opacity: 1;
    transform: translate(-50%, 0);
  }
  100% {
    opacity: 0;
    transform: translate(-50%, -100px); /* Увеличили расстояние */
  }
}

/* Стили для облачка с сообщением */
.chat-bubble {
  position: absolute;
  top: -10px; /* Позиция над монеткой */
  right: -50px; /* Сдвигаем влево (было -200px) */
  background-color: rgba(255, 255, 255, 0.9); /* Белый фон с прозрачностью */
  color: #333; /* Цвет текста */
  padding: 10px 15px;
  border-radius: 15px;
  font-family: Geologica;
  font-size: 16px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); /* Тень для эффекта облачка */
  animation: fadeInOut 2s ease-in-out; /* Анимация появления и исчезновения */
}

/* Анимация появления и исчезновения */
@keyframes fadeInOut {
  0% {
    opacity: 0;
    transform: translateY(10px);
  }
  10% {
    opacity: 1;
    transform: translateY(0);
  }
  90% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateY(10px);
  }
}

/* Анимация исчезновения +1 */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

/* Стили для нижней панели */
.bar {
  background-color: #2c2c2e;
  position: fixed;
  bottom: 0;
  left: -5px; /* Сдвигаем панель влево на 20px */
  width: 100%;
  height: 45px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  border-top-left-radius: 30px;
  border-top-right-radius: 30px;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.2);
}

.bar .nav-item {
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 1;
}

.bar .nav-item.active img {
  filter: brightness(1.5);
}

.bar button {
  background: none;
  border: none;
  color: white;
  font-size: 16px;
}

.bar img {
  cursor: pointer;
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
const isShaking = ref(false); // Для анимации тряски
const showPlusOne = ref(false); // Для отображения +1
const showFastTapMessage = ref(false); // Для отображения сообщения
const lastTapTime = ref(0); // Время последнего клика

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

    // Анимация тряски и +1
    isShaking.value = true;
    showPlusOne.value = true;

    // Сбрасываем анимацию тряски через 200 мс
    setTimeout(() => {
      isShaking.value = false;
    }, 200);

    // Скрываем +1 через 800 мс
    setTimeout(() => {
      showPlusOne.value = false;
    }, 800);

    // Проверка на быстрый клик
    const currentTime = Date.now();
    if (currentTime - lastTapTime.value < 300) {
      showFastTapMessage.value = true;
      setTimeout(() => {
        showFastTapMessage.value = false;
      }, 2000); // Скрываем сообщение через 2 секунды
    }
    lastTapTime.value = currentTime; // Обновляем время последнего клика
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
