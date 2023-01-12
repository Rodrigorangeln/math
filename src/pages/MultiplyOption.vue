<template>
  <!-- <q-page class="flex flex-center">
      <img alt="Quasar logo" src="../assets/logo.svg" style="width: 200px; height: 200px">
    </q-page> -->
  <div class="q-pa-md">
    <q-card class="bg-yellow-3">
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
      <q-card-section ref="msg" class="text-center">
        {{ msg }}
      </q-card-section>
      <tr class="row text-h2 text-weight-bold justify-between q-pa-md">
        <!-- <td v-for="option in options" :key="option">
          {{ option }}
        </td> -->
        <td @click="selected(options[0])">{{ options[0] }}</td>
        <td>{{ options[1] }}</td>
        <td>{{ options[2] }}</td>
      </tr>
      <tr class="row text-h2 text-weight-bold justify-between q-pa-md">
        <td>{{ options[3] }}</td>
        <td>{{ options[4] }}</td>
        <td>{{ options[5] }}</td>
      </tr>
    </q-card>
  </div>
</template>

  <script>
import { ref, defineComponent } from 'vue';

export default defineComponent({
  name: 'MultiplyOption',

  setup() {
    const random = (param = 10) => {
      let randomNumber = Math.floor(Math.random() * param) + 2;
      return randomNumber;
    };

    let number = ref({
      a: random(),
      b: random(),
    });
    let answer = ref(number.value.a * number.value.b);
    let options = ref([]);
    let msg = ref('Escolha sua resposta').value;

    for (var i = 0; i < 5; i++) {
      options.value.push(distractors(i));
    }
    options.value.push(answer.value);
    shuffleArray(options.value);

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

    function selected(param) {
      alert(param);
    }

    return {
      number,
      //answer,
      msg,
      options,
      selected,
    };
  },
});
</script>
