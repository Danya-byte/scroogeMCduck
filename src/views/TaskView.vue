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
        <li v-for="(item) in data" :key="item.id">
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
            <h1 class="start-button" @click="handleStart(item)">Start</h1>
          </div>
        </li>
      </ul>
    </section>

    <!-- Нижняя панель навигации -->
    <div class="bar">
      <RouterLink to="/task" class="nav-item" :class="{ active: $route.path === '/task' }">
        <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px">
        <button class="task"></button>
      </RouterLink>
      <RouterLink to="/" class="nav-item" :class="{ active: $route.path === '/' }">
        <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px">
        <button class="game"></button>
      </RouterLink>
      <RouterLink to="/leader" class="nav-item" :class="{ active: $route.path === '/leader' }">
        <img src="https://i.postimg.cc/fRPzxjgn/0-F65-F8-E0-D77-D-464-C-B669-07-F0287-ABD7-C.png" width="50px">
        <button class="soon"></button>
      </RouterLink>
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
}

.bar {
  background-color: #2c2c2e;
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 45px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
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

.start-button:hover {
  background-color: #3390ec;
  color: white;
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
        },
        {
          id: 2,
          type: 'Transaction',
          reward: '+10 $FUCK',
          link: 'https://t.me/blum/app?startapp=memepadjetton_SCMD69_Stje1-ref_2rrmsdCh93',
        },
        {
          id: 3,
          type: 'Channel',
          reward: '+15 $FUCK',
          link: 'https://t.me/FreeScroogy69',
        },
        {
          id: 4,
          type: 'TEST',
          reward: '+15 $FUCK',
          link: 'https://example.com/test',
        },
      ],
    };
  },
  methods: {
    handleStart(item) {
      // Обработка клика в зависимости от типа задачи
      switch (item.type) {
        case 'Channel':
          window.open(item.link, '_blank');
          break;
        case 'Transaction':
          this.performTransaction(item);
          break;
        case 'Partners':
          window.open(item.link, '_blank');
          break;
        default:
          console.log('Неизвестный тип задачи:', item.type);
      }
    },
    performTransaction(item) {
      // Пример выполнения транзакции
      console.log('Transaction to:', item);
      this.showMessages(`Transaction completed! Награда: ${item.reward}`);
    },
    showMessages(message) {
      // Пример реализации показа сообщения (можно заменить на toast или модальное окно)
      const messageElement = document.createElement('div');
      messageElement.style.position = 'fixed';
      messageElement.style.bottom = '20px';
      messageElement.style.right = '20px';
      messageElement.style.backgroundColor = '#3390ec';
      messageElement.style.color = 'white';
      messageElement.style.padding = '10px 20px';
      messageElement.style.borderRadius = '5px';
      messageElement.style.zIndex = '1000';
      messageElement.textContent = message;

      document.body.appendChild(messageElement);

      // Удаление сообщения через 3 секунды
      setTimeout(() => {
        document.body.removeChild(messageElement);
      }, 3000);
    },
  },
};
</script>
