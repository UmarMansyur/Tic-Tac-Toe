<script setup lang="ts">
import { onMounted, ref } from "vue";
const player = ref<1 | 2>(1);
const boxes = ref<number[][]>([
  [0, 0, 0],
  [0, 0, 0],
  [0, 0, 0],
]);

function playerClick(x: number, y: number) {
  if (boxes.value[x][y] != 0) {
    return;
  }

  if (player.value == 1) {
    boxes.value[x][y] = 1;
  } else {
    boxes.value[x][y] = 2;
  }
  winner();
  player.value = player.value == 1 ? 2 : 1;
}

function classIcon(x: number, y: number) {
  if (boxes.value[x][y] == 1) {
    return "fa-sharp fa-solid fa-xmark";
  }
  if (boxes.value[x][y] == 2) {
    return "fa-regular fa-circle";
  }
  return "";
}

function classBox(x: number, y: number) {
  if (boxes.value[x][y] == 1) {
    return "red-box";
  }
  if (boxes.value[x][y] == 2) {
    return "yellow-box";
  }
  return "";
}

function winner() {
  // check tictactoe winner
  // check rows
  for (let a = 0; a < 3; a++) {
    if (boxes.value[a].join("") === "111") {
      alertReset(1);
    } else {
      if (boxes.value[a].join("") === "222") {
        alertReset(2);
      }
    }
  }
  for (let a = 0; a < 3; a++) {
    if (
      boxes.value[0][a] == boxes.value[1][a] &&
      boxes.value[1][a] == boxes.value[2][a]
    ) {
      if (boxes.value[0][a] == 1) {
        alertReset(1);
      } else {
        if (boxes.value[0][a] == 2) {
          alertReset(2);
        }
      }
    }
  }
  if ( boxes.value[0][0] == boxes.value[1][1] && boxes.value[1][1] == boxes.value[2][2]) {
    if (boxes.value[0][0] == 1) {
      alertReset(1);
    } else {
      if (boxes.value[0][0] == 2) {
        alertReset(2);
      }
    }
  }
  if ( boxes.value[0][2] == boxes.value[1][1] && boxes.value[1][1] == boxes.value[2][0]) {
    if (boxes.value[0][2] == 1) {
      alertReset(1);
    } else{
      if (boxes.value[0][2] == 2) {
        alertReset(2);
      }
    }
  }
}

function alertReset(p: number) {
  console.log(p);
  setTimeout(() => {
    alert(`Player ${p} wins`);
    reset();
  }, 300);
}

function reset() {
  boxes.value = [
    [0, 0, 0],
    [0, 0, 0],
    [0, 0, 0],
  ];
  player.value = 1;
}
</script>
<template>
  <div class="container">
    <!-- judul -->
    <section class="title">
      <h1>Tic Tac Toe</h1>
    </section>
    <!-- papan -->
    <section class="main">
      <div class="kotak">
        <button
          class="kotakKlik bottom-border"
          @click="playerClick(0, 0)"
          :class="classBox(0, 0)"
          type="button"
        >
          <i :class="classIcon(0, 0)"></i>
        </button>
        <button
          class="kotakKlik left-right-border bottom-border"
          @click="playerClick(0, 1)"
          :class="classBox(0, 1)"
        >
          <i :class="classIcon(0, 1)"></i>
        </button>
        <button
          @click="playerClick(0, 2)"
          :class="classBox(0, 2)"
          class="kotakKlik bottom-border"
        >
          <i :class="classIcon(0, 2)"></i>
        </button>
        <button
          @click="playerClick(1, 0)"
          :class="classBox(1, 0)"
          class="kotakKlik bottom-border"
        >
          <i :class="classIcon(1, 0)"></i>
        </button>
        <button
          @click="playerClick(1, 1)"
          :class="classBox(1, 1)"
          class="kotakKlik left-right-border bottom-border"
        >
          <i :class="classIcon(1, 1)"></i>
        </button>
        <button
          @click="playerClick(1, 2)"
          :class="classBox(1, 2)"
          class="kotakKlik bottom-border"
        >
          <i :class="classIcon(1, 2)"></i>
        </button>
        <button
          @click="playerClick(2, 0)"
          :class="classBox(2, 0)"
          class="kotakKlik"
        >
          <i :class="classIcon(2, 0)"></i>
        </button>
        <button
          @click="playerClick(2, 1)"
          :class="classBox(2, 1)"
          class="kotakKlik left-right-border"
        >
          <i :class="classIcon(2, 1)"></i>
        </button>
        <button
          @click="playerClick(2, 2)"
          :class="classBox(2, 2)"
          class="kotakKlik"
        >
          <i :class="classIcon(2, 2)"></i>
        </button>
      </div>
    </section>
    <!-- tombol -->
    <section class="tombol">
      <button class="player">Player {{ player }}</button>
      <button class="player reset" @click="reset()">Reset</button>
    </section>
  </div>
</template>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Pacifico&display=swap");
body {
  margin: 0;
  padding: 0;
}

.container {
  margin: 0;
  padding: 0;
  width: 100vw;
  display: flex;
  flex-direction: column;
  height: 100vh;
  .title {
    height: 170px;
    display: flex;
    h1 {
      line-height: 0.5;
      font-size: 68px;
      width: 100%;
      text-align: center;
      font-family: "Pacifico", cursive;
    }
  }

  .main {
    display: flex;
    flex-grow: 1;
    justify-content: center;
    align-items: center;
    background-color: white;
    .kotak {
      height: 409px;
      width: 409px;
      .kotakKlik {
        background-color: white;
        display: inline-block;
        vertical-align: middle;
        font-size: 90px;
        color: #f24e1e;
        border: none;
        height: 133px;
        width: 133px;
        &.left-right-border {
          border-left: 5px solid #14bdac;
          border-right: 5px solid #14bdac;
          width: 143px;
        }
        &.bottom-border {
          height: 138px;
          border-bottom: 5px solid #14bdac;
        }
        &.red-box {
          line-height: 1;
          color: #f24e1e;
        }
        &.yellow-box {
          color: #f8e32b;
          line-height: 0;
          i {
            font-size: 65px;
          }
        }
      }
    }
  }

  .tombol {
    height: 170px;
    display: flex;
    justify-content: center;
    align-items: center;
    .player {
      margin: 0 12px;
      font-family: "Pacifico", cursive;
      font-size: 32px;
      color: white;
      width: 302px;
      height: 73px;
      background: #f47e7e;
      border-color: white;
      border-width: 0;
      border-radius: 34px;
      &.reset {
        background: #27aaff;
      }
    }
  }
}
</style>
