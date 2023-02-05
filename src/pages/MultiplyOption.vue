<template>
  <!-- <q-page class="flex flex-center">
      <img alt="Quasar logo" src="../assets/logo.svg" style="width: 200px; height: 200px">
    </q-page> -->

  <q-dialog v-model="alert">
    <q-card>
      <q-card-section>
        <div class="text-h6">Você teve {{ score }} acertos!</div>
      </q-card-section>

      <q-card-actions align="center">
        <q-btn flat label="OK" color="primary" v-close-popup />
      </q-card-actions>
    </q-card>
  </q-dialog>

  <div class="q-pa-md">
    <q-card class="bg-yellow-3">
      <q-btn flat :class="aniHeart"> ❤️ {{ lifes }} </q-btn>
      <q-btn flat><q-icon color="green" name="check" /> {{ score }} </q-btn>
      <q-card-section class="text-right q-mr-xl">
        <div class="text-h1 text-weight-bold">{{ number.a }}</div>
        <div class="row justify-between">
          <div ref="operation" class="text-h2 text-weight-bold q-mt-lg q-ml-xl">
            x
          </div>
          <div class="text-h1 text-weight-bold">{{ number.b }}</div>
        </div>
      </q-card-section>
      <q-separator inset size="0.3rem" color="dark" />
      <!-- <q-card-section class="text-center" :class="selected ? 'text-h3' : ''">
        {{ selected ? selected : msg }}
      </q-card-section> -->
      <tr class="row text-h2 text-weight-bold justify-between q-pa-md">
        <div
          v-for="(option, index) in options"
          :key="index"
          class="col-4 text-center"
        >
          <q-btn
            :class="selected == option ? 'selected' : ''"
            @click="selected = option"
            size="0.9em"
            flat
            >{{ option }}</q-btn
          >
        </div>
      </tr>
      <q-btn
        color="secondary"
        :label="labelBtn"
        @click="labelBtn == 'Começar' ? start() : toCheck()"
        class="q-mb-sm full-width"
      />
    </q-card>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import 'animate.css';

let number = ref({
  a: 0,
  b: 0,
});

const answer = ref();
const options = ref([]);
//const msg = ref('Escolha sua resposta');
const selected = ref('');
const lifes = ref(3);
const score = ref(0);
const alert = ref(false);
let labelBtn = ref('Começar');
let aniHeart = ref(null);

function toCheck() {
  if (selected.value == answer.value) {
    ++score.value;
    this.start();
  } else if (lifes.value > 0) {
    --lifes.value;
    aniHeart.value = 'animate__animated animate__shakeY';
  } else {
    alert.value = true;
  }
}

function start() {
  this.number.a = random();
  this.number.b = random();
  this.answer = number.value.a * number.value.b;

  options.value = [];
  for (var i = 0; i < 5; i++) {
    options.value.push(distractors(i));
  }
  options.value.push(answer.value);
  shuffleArray(options.value);
  this.labelBtn = 'OK';
}

const random = (param = 9) => {
  let randomNumber = Math.floor(Math.random() * param) + 2;
  return randomNumber;
};

function distractors(i) {
  if (i < 3) {
    return answer.value + random();
  } else {
    return answer.value - random();
  }
}

function shuffleArray(array) {
  for (let i = 0; i < array.length; i++) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}
</script>

<style scoped>
.selected {
  color: rgb(27, 8, 138);
  font-weight: bold;
}
</style>

