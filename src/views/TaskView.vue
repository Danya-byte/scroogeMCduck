<template>
  <div class="task-board">
    <!-- Заголовок и картинка -->
    <div style="display: grid; align-items: center; justify-content: center; margin-top: 20px;">
      <img width="65px" height="65px" src="https://em-content.zobj.net/source/telegram/386/sparkles_2728.webp" />
    </div>
    <div class="leader-title">
      <h1 style="color: #f0f0f0; text-align: center;">Tasks</h1>
    </div>

    <!-- Список задач -->
    <section class="tasks">
      <ul class="refs">
        <li v-for="(item) in data" :key="item.id">
          <div class="about">
            <div style="display: flex; align-items: center; justify-content: center;">
              <img
                v-if="item.type == 'Channel'"
                style="border-radius: 50px;"
                width="40px"
                height="40px"
                src="https://i.postimg.cc/mZnL0Gsf/2-C2-FD02-E-0-BB2-4-E91-A52-A-FAF4-BB160-FD3.png"
              />
              <img
                v-if="item.type == 'Transaction'"
                style="border-radius: 50px;"
                width="40px"
                height="40px"
                src="https://i.postimg.cc/gj5cjhgV/CF8-B7771-2095-45-F1-AF17-ADE4-D690-A29-E.png.png"
              />
            </div>
            <div>
              <h3 style="font-family: Quicksand; color: #fff;">{{ item.type }}</h3>
              <p style="padding: 0; font-size: 14px; color: #aaaaaa; background: 0;">{{ item.reward }}</p>
            </div>
          </div>
          <div style="display: grid; align-items: center;">
            <h1 style="font-family: Quicksand; font-size: 18px; font-weight: 600; color: #3390ec;">Start</h1>
          </div>
        </li>
      </ul>
    </section>

    <!-- Нижняя панель навигации -->
    <div class="bar">
      <RouterLink to="/task">
        <img src="https://i.postimg.cc/kGxp19cP/5-CFA8313-0975-4-AE0-9986-E13-E9-B754-C11.png" width="40px" style="position: absolute; margin-left: 50vw; margin-top: 1vw">
        <button class="task"></button>
      </RouterLink>
      <RouterLink to="/">
        <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px" style="position: absolute; margin-left: 8vw;">
        <button class="game"></button>
      </RouterLink>
      <RouterLink to="/leader">
        <img src="https://i.postimg.cc/fRPzxjgn/0-F65-F8-E0-D77-D-464-C-B669-07-F0287-ABD7-C.png" width="50px" style="position: absolute; margin-left: 12vw; margin-top: 3vw">
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
  overflow-y: auto; /* Добавляем прокрутку, если контент не помещается */
}

.leader-title h1 {
  margin-top: 10px;
  font-size: 24px;
}

.refs {
  margin-top: 15px;
  display: grid;
  gap: 20px;
  padding: 0 20px; /* Добавляем отступы по бокам */
}

.refs li {
  padding: 0 5px 20px 5px;
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #181818;
}

.about {
  display: flex;
  gap: 10px;
  align-items: center;
}

.tasks {
  padding: 10px;
  margin-top: 10px;
  display: grid;
  gap: 20px;
}

.bar {
  background-color: #2c2c2e;
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 80px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
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

<script>
export default {
  data() {
    return {
      data: [
        {
          id: 1,
          type: 'Channel',
          reward: '+500 EWE',
        },
        {
          id: 2,
          type: 'Channel',
          reward: '+1000 EWI',
        },
      ],
    };
  },
};
</script>
