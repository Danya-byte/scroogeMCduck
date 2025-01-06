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

    <!-- Модальное окно и сообщение об успехе (остается без изменений) -->
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
      showModal: false,
      showSuccessMessage: false,
      currentLink: '',
      currentReward: '',
      taskCompleted: false,
      currentTaskImage: '',
    };
  },
  methods: {
    handleStart(item) {
      switch (item.type) {
        case 'Channel':
        case 'Partners':
          this.openTelegramLink(item.link);
          this.currentLink = item.link;
          this.currentReward = item.reward;
          this.currentTaskImage = this.getTaskImage(item.type);
          this.showModal = true;
          break;
        case 'Transaction':
          this.openTelegramLink(item.link);
          this.currentReward = item.reward;
          this.showSuccessMessage = true;
          setTimeout(() => {
            this.showSuccessMessage = false;
          }, 3000);

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
      if (window.Telegram && window.Telegram.WebApp) {
        window.Telegram.WebApp.openLink(url, { try_instant_view: true });
      } else {
        window.open(url, '_blank');
      }
    },
    handleCheck() {
      this.taskCompleted = true;
      this.showSuccessMessage = true;
      setTimeout(() => {
        this.showSuccessMessage = false;
      }, 3000);

      const task = this.data.find((t) => t.link === this.currentLink);
      if (task) {
        task.completed = true;
      }

      this.showModal = false;
    },
    handleGo() {
      this.openTelegramLink(this.currentLink);
    },
  },
};
</script>
