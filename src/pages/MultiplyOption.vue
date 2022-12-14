<template>
  <!-- <q-page class="flex flex-center">
      <img alt="Quasar logo" src="../assets/logo.svg" style="width: 200px; height: 200px">
    </q-page> -->
  <div class="q-pa-md">
    <q-card class="bg-yellow-3">
      <q-card-section class="text-right q-mr-xl">
        <div class="text-h1 text-weight-bold">{{ aRandom }}</div>
        <div class="row justify-between">
          <div ref="operation" class="text-h2 text-weight-bold q-mt-lg q-ml-xl">
            x
          </div>
          <div class="text-h1 text-weight-bold">{{ bRandom }}</div>
        </div>
      </q-card-section>
      <q-separator inset size="0.3rem" color="dark" />
      <q-card-section ref="msg" class="text-center">
        Escolha sua resposta
      </q-card-section>
      <div class="row text-h2 text-weight-bold justify-between q-pa-md">
        <div>0</div>
        <div>0</div>
        <div>0</div>
      </div>
      <div class="row text-h2 text-weight-bold justify-between q-pa-md">
        <div>0</div>
        <div>0</div>
        <div>0</div>
      </div>
    </q-card>
  </div>
</template>

  <script>
//import { reactive } from 'vue';

export default {
  name: 'MultiplyOption',

  setup() {
    const random = (param = 10) => {
      let randomNumber = Math.floor(Math.random() * param) + 2;
      return randomNumber;
    };
    let aRandom = random();
    let bRandom = random();
    let answer = aRandom * bRandom;
    console.log('>>>>>' + answer);

    return {
      aRandom,
      bRandom,
      answer,
    };
  },
};
</script>
