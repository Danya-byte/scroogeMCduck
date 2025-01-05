<template>
  <div class="content-container">
    <center>
      <img src="https://em-content.zobj.net/source/telegram/386/money-bag_1f4b0.webp" width="220px" style="margin-top: 50px;">
    </center>
    <h1 style="color: white; font-family: Geologica;">Task</h1>
    <div class="backtask">
      <img src="https://i.postimg.cc/mZnL0Gsf/2-C2-FD02-E-0-BB2-4-E91-A52-A-FAF4-BB160-FD3.png" width="50px" style="margin-top: 10px; margin-left: 5px;">
      <h3 style="position: absolute; margin-top: -40px; margin-left: 70px; color: white; font-family: Geologica;">Check Channel</h3>
      <a href="https://t.me/Greenwoods_Community" target="_blank"><button class="check">Check</button></a>
    </div>
    <div class="backtask" style="margin-top: 10px;">
      <img src="https://i.postimg.cc/gj5cjhgV/CF8-B7771-2095-45-F1-AF17-ADE4-D690-A29-E.png" width="50px" style="margin-top: 10px; margin-left: 5px;">
      <h3 style="position: absolute; margin-top: -40px; margin-left: 70px; color: white; font-family: Geologica;">Check Channel</h3>
      <a href="https://t.me/FreeScroogy69" target="_blank"><button class="check">Check</button></a>
    </div>
    <div class="backtask" style="margin-top: 10px;">
      <img src="https://i.postimg.cc/xCj2Qkp5/2587-D1-A6-37-E0-45-B0-89-E4-3-F4-D29-E83130.png" width="50px" style="margin-top: 10px; margin-left: 5px;">
      <h3 style="position: absolute; margin-top: -40px; margin-left: 70px; color: white; font-family: Geologica;">Buy Token</h3>
      <a href="https://t.me/blum/app?startapp=memepadjetton_SCMD69_Stje1-ref_2rrmsdCh93" target="_blank"><button class="check">Buy</button></a>
    </div>
  </div>

  <div class="bar">
    <RouterLink to="/task">
      <img src="https://i.postimg.cc/MKmL16Hy/3164-B3-A9-E06-A-42-A6-82-DC-1-AFA9-B7095-E8.png" width="40px" style="position: absolute; margin-left: 50vw; margin-top: 1vw">
      <button class="task"></button>
    </RouterLink>
    <RouterLink to="/">
      <img src="https://i.postimg.cc/66MKNfLs/D81-A5-CE1-57-CE-4417-A490-91-BCEF9-F5-B68.png" width="55px" style="position: absolute; margin-left: 8vw;">
      <button class="game"></button>
    </RouterLink>
    <RouterLink to="/leader">
      <img src="https://i.postimg.cc/tCz2cBhP/D384540-F-C585-455-C-AAB5-D10-FA58774-B2.png" width="50px" style="position: absolute; margin-left: 12vw; margin-top: 3vw">
      <button class="soon"></button>
    </RouterLink>
  </div>
</template>

<style scoped>
body {
  font-family: Geologica;
  background-color: #3b3b3b;
  color: white;
  touch-action: none;
  overflow-y: scroll;
}

.content-container {
  height: 80vh; /* Задайте высоту контейнера, чтобы он занимал 80% высоты экрана */
  overflow-y: scroll; /* Включите вертикальную прокрутку */
  padding-bottom: 100px; /* Добавьте отступ снизу, чтобы контент не перекрывался с нижней панелью */
}

.check {
  background-color: rgb(105, 175, 237);
  border: none;
  border-radius: 25px;
  color: white;
  width: 60px;
  height: 30px;
  position: absolute;
  margin-left: 65vw;
  margin-top: 20px;
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

.task {
  background-color: #2c2c2e;
  width: 33vw;
  height: 105px;
  border: none;
  font-family: Geologica;
  color: white;
  margin-left: 38vw;
  color: rgb(17, 117, 193);
}

.game {
  background-color: #2c2c2e;
  width: 33vw;
  height: 100px;
  border: none;
  font-family: Geologica;
  color: white;
  margin-left: -2vw;
  color: rgb(82, 82, 82);
}

.soon {
  background-color: #2c2c2e;
  width: 38vw;
  height: 105px;
  border: none;
  font-family: Geologica;
  color: white;
  margin-left: -1vw;
  color: rgb(82, 82, 82);
}

.backtask {
  background-color: #2c2c2e;
  height: 70px;
  border-radius: 15px;
}
</style>
