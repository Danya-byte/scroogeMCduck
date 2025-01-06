<template>
  <div class="task-board">
    <!-- Заголовок и картинка -->
    <div style="display: grid; align-items: center; justify-content: center; margin-top: 50px;">
      <img width="90px" height="90px" src="https://em-content.zobj.net/source/telegram/386/sparkles_2728.webp" />
    </div>
    <div class="leader-title" style="margin-top: 25px;">
      <h1 style="color: #f0f0f0; text-align: center;">Tasks</h1>
    </div>

    <!-- Список задач -->
    <section class="tasks" style="margin-top: 40px;">
      <ul class="refs">
        <li v-for="(item) in data" :key="item.id" :class="{ 'completed-task': item.completed }">
          <div class="about">
            <div style="display: flex; align-items: center; justify-content: center;">
              <img
                v-if="item.type == 'Channel'"
                style="border-radius: 50px;"
                width="50px"
                height="50px"
                src="https://i.postimg.cc/xCj2Qkp5/2587-D1-A6-37-E0-45-B0-89-E4-3-F4-D29-E83130.png"
              />
              <img
                v-if="item.type == 'Transaction'"
                style="border-radius: 50px;"
                width="50px"
                height="50px"
                src="https://i.postimg.cc/gj5cjhgV/CF8-B7771-2095-45-F1-AF17-ADE4-D690-A29-E.png.png"
              />
              <img
                v-if="item.type == 'Partners'"
                style="border-radius: 50px;"
                width="50px"
                height="50px"
                src="https://i.postimg.cc/mZnL0Gsf/2-C2-FD02-E-0-BB2-4-E91-A52-A-FAF4-BB160-FD3.png"
              />
            </div>
            <div>
              <h3 style="font-family: Quicksand; color: #fff; font-size: 20px;">{{ item.type }}</h3>
              <p style="padding: 0; font-size: 17px; color: #aaaaaa; background: 0;">{{ item.reward }}</p>
            </div>
          </div>
          <div style="display: grid; align-items: center;">
            <h1
              class="start-button"
              :class="{ disabled: item.completed }"
              @click="!item.completed && handleStart(item)"
            >
              {{ item.completed ? 'Completed' : 'Start' }}
            </h1>
          </div>
          <div v-if="item.completed" class="fireworks"></div>
        </li>
      </ul>
    </section>

    <!-- Нижняя панель навигации -->
    <div class="bar">
      <RouterLink to="/task" class="nav-item" :class="{ active: $route.path === '/task' }" exact>
        <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px">
        <button class="task"></button>
      </RouterLink>
      <RouterLink to="/" class="nav-item" :class="{ active: $route.path === '/' }" exact>
        <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px">
        <button class="game"></button>
      </RouterLink>
      <RouterLink to="/leader" class="nav-item" :class="{ active: $route.path === '/leader' }" exact>
        <img src="https://i.postimg.cc/fRPzxjgn/0-F65-F8-E0-D77-D-464-C-B669-07-F0287-ABD7-C.png" width="50px">
        <button class="soon"></button>
      </RouterLink>
    </div>

    <!-- Модальное окно после возвращения из канала или партнеров -->
    <div v-if="showModal" class="modal-overlay">
      <div class="modal">
        <div class="modal-content">
          <img
            :src="currentTaskImage"
            width="80px"
            height="80px"
            style="border-radius: 50%;"
          />
          <p style="margin-top: 10px; font-size: 16px; color: #fff;">Подпишитесь на канал:</p>
          <a :href="currentLink" target="_blank" style="color: #3390ec; text-decoration: none;">{{ currentLink }}</a>
          <div style="display: flex; gap: 10px; margin-top: 20px;">
            <button class="modal-button check" @click="handleCheck">Check</button>
            <button class="modal-button go" @click="handleGo">Go</button>
          </div>
        </div>
      </div>
    </div>

    <!-- Сообщение об успешном присоединении -->
    <div v-if="showSuccessMessage" class="success-message-container">
      <div class="fireworks left"></div>
      <div class="success-message">
        <p>Reward: {{ currentReward }}</p>
      </div>
      <div class="fireworks right"></div>
    </div>
  </div>
</template>

<style scoped>
.task-board {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: #212121;
  overflow-y: auto;
}

.leader-title h1 {
  margin-top: 10px;
  font-size: 24px;
}

.refs {
  margin-top: 15px;
  display: grid;
  gap: 3px;
  padding: 0 20px;
}

.refs li {
  width: 100%;
  padding: 0 5px 15px 5px;
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #181818;
  border: 1px solid #444444;
  border-radius: 10px;
  padding: 10px;
  position: relative;
}

.about {
  display: flex;
  gap: 10px;
  align-items: center;
}

.tasks {
  padding: 10px;
  margin-top: 30px;
  padding-bottom: 30px;
  display: grid;
  gap: 5px;
  max-width: 800px; /* Ограничиваем максимальную ширину контейнера задач */
  margin-left: auto; /* Центрируем контейнер */
  margin-right: auto; /* Центрируем контейнер */
}

.bar {
  background-color: #2c2c2e;
  position: fixed;
  bottom: 0;
  left: -5px;
  width: 100%;
  height: 45px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  border-top-left-radius: 30px; /* Скругление слева */
  border-top-right-radius: 30px; /* Скругление справа */
}

.bar .nav-item {
  display: flex;
  align-items: center;
  justify-content: center;
  flex: 1;
}

.bar .nav-item.active img {
  filter: brightness(1.5); /* Подсветка активной иконки */
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

/* Стили для кнопки Start */
.start-button {
  font-family: Quicksand;
  font-size: 18px;
  font-weight: 600;
  color: #3390ec;
  border: 2px solid #3390ec;
  border-radius: 25px;
  padding: 8px 20px;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
}

.start-button.disabled {
  background-color: #444444;
  color: #777777;
  cursor: not-allowed;
}

.start-button:hover:not(.disabled) {
  background-color: #3390ec;
  color: white;
}

/* Модальное окно */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: flex-end; /* Окно снизу */
  z-index: 1000;
}

.modal {
  background: #2c2c2e;
  border-radius: 20px 20px 0 0; /* Скругленные углы сверху */
  padding: 20px;
  width: 100%;
  max-width: 500px;
  text-align: center;
}

.modal-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.modal-button {
  padding: 10px 20px;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.modal-button.check {
  background-color: #3390ec;
  color: white;
}

.modal-button.check:hover {
  background-color: #2a7bbf;
}

.modal-button.go {
  background-color: #444444;
  color: white;
}

.modal-button.go:hover {
  background-color: #555555;
}

/* Сообщение об успешном присоединении */
.success-message-container {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.success-message {
  background: #3390ec;
  color: white;
  padding: 20px;
  border-radius: 10px;
  animation: fadeInOut 3s ease-in-out;
  position: relative;
  z-index: 2;
}

@keyframes fadeInOut {
  0% { opacity: 0; }
  10% { opacity: 1; }
  90% { opacity: 1; }
  100% { opacity: 0; }
}

/* Анимация салюта */
.fireworks {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100px;
  height: 100px;
  z-index: 1;
  pointer-events: none;
}

.fireworks.left {
  left: -120px; /* Салют слева от сообщения */
}

.fireworks.right {
  right: -120px; /* Салют справа от сообщения */
}

.fireworks::before,
.fireworks::after {
  content: '';
  position: absolute;
  width: 20px;
  height: 20px;
  background: url('https://emojipedia-us.s3.dualstack.us-west-1.amazonaws.com/thumbs/120/apple/325/sparkles_2728.png') no-repeat center center;
  background-size: contain;
  animation: fireworksAnimation 1s ease-in-out;
}

.fireworks.left::before {
  top: 0;
  left: 0;
  animation-delay: 0s;
}

.fireworks.left::after {
  top: 50%;
  left: 50%;
  animation-delay: 0.5s;
}

.fireworks.right::before {
  top: 0;
  right: 0;
  animation-delay: 0s;
}

.fireworks.right::after {
  top: 50%;
  right: 50%;
  animation-delay: 0.5s;
}

@keyframes fireworksAnimation {
  0% { transform: translateY(0) scale(0); opacity: 0; }
  50% { transform: translateY(-50px) scale(1); opacity: 1; }
  100% { transform: translateY(-100px) scale(0); opacity: 0; }
}

/* Зеленая галочка и прозрачный зеленый фон */
.completed-overlay {
  background: rgba(76, 175, 80, 0.3); /* Прозрачный зеленый */
  border-radius: 50%;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Стили для завершенных задач */
.completed-task {
  position: relative;
  overflow: hidden;
}

.completed-task::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(76, 175, 80, 0.3); /* Прозрачный зеленый */
  z-index: 1;
}

.completed-task .start-button {
  background-color: #4CAF50; /* Зеленый цвет для кнопки */
  color: white;
  cursor: not-allowed;
}
</style>

<script>
export default {
  data() {
    return {
      data: [
        {
          id: 1,
          type: 'Partners',
          reward: '+5 $FUCK',
          link: 'https://t.me/Greenwoods_Community',
          completed: false,
        },
        {
          id: 2,
          type: 'Transaction',
          reward: '+10 $FUCK',
          link: 'https://t.me/blum/app?startapp=memepadjetton_SCMD69_Stje1-ref_2rrmsdCh93',
          completed: false,
        },
        {
          id: 3,
          type: 'Channel',
          reward: '+15 $FUCK',
          link: 'https://t.me/FreeScroogy69',
          completed: false,
        },
        {
          id: 4,
          type: 'TEST',
          reward: '+15 $FUCK',
          link: 'https://example.com/test',
          completed: false,
        },
      ],
      showModal: false, // Показывать ли модальное окно
      showSuccessMessage: false, // Показывать ли сообщение об успехе
      currentLink: '', // Текущая ссылка для модального окна
      currentReward: '', // Текущая награда для сообщения
      taskCompleted: false, // Задача выполнена
      currentTaskImage: '', // Переменная для хранения текущей картинки
    };
  },
  methods: {
    handleStart(item) {
      // Обработка клика в зависимости от типа задачи
      switch (item.type) {
        case 'Channel':
        case 'Partners':
          this.openTelegramLink(item.link);
          this.currentLink = item.link; // Сохраняем ссылку для модального окна
          this.currentReward = item.reward; // Сохраняем награду
          this.currentTaskImage = this.getTaskImage(item.type); // Устанавливаем картинку для модального окна
          this.showModal = true; // Показываем модальное окно после возвращения
          break;
        case 'Transaction':
          this.openTelegramLink(item.link); // Переход по ссылке
          this.currentReward = item.reward; // Сохраняем награду
          this.showSuccessMessage = true; // Показываем сообщение о награде
          setTimeout(() => {
            this.showSuccessMessage = false;
          }, 3000);

          // Помечаем задачу как выполненную
          const task = this.data.find((t) => t.id === item.id);
          if (task) {
            task.completed = true;
          }
          break;
        default:
          console.log('Неизвестный тип задачи:', item.type);
      }
    },
    getTaskImage(type) {
      // Возвращаем картинку в зависимости от типа задачи
      switch (type) {
        case 'Channel':
          return 'https://i.postimg.cc/xCj2Qkp5/2587-D1-A6-37-E0-45-B0-89-E4-3-F4-D29-E83130.png';
        case 'Partners':
          return 'https://i.postimg.cc/mZnL0Gsf/2-C2-FD02-E-0-BB2-4-E91-A52-A-FAF4-BB160-FD3.png';
        default:
          return '';
      }
    },
    openTelegramLink(url) {
      // Используем метод Telegram WebApp для открытия ссылки
      if (window.Telegram && window.Telegram.WebApp) {
        window.Telegram.WebApp.openLink(url, { try_instant_view: true });
      } else {
        // Если мини-приложение Telegram не доступно, открываем ссылку в новой вкладке
        window.open(url, '_blank');
      }
    },
    handleCheck() {
      // Обработка нажатия на кнопку Check
      this.taskCompleted = true; // Задача выполнена
      this.showSuccessMessage = true; // Показываем сообщение об успехе
      setTimeout(() => {
        this.showSuccessMessage = false;
      }, 3000);

      // Помечаем задачу как выполненную
      const task = this.data.find((t) => t.link === this.currentLink);
      if (task) {
        task.completed = true;
      }

      // Закрываем модальное окно
      this.showModal = false;
    },
    handleGo() {
      // Обработка нажатия на кнопку Go
      this.openTelegramLink(this.currentLink); // Открываем ссылку через Telegram WebApp
    },
  },
};
</script>
