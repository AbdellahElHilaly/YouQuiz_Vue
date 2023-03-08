<script setup>
import { ref, markRaw } from 'vue'
import SteperCompe from '@/components/SteperComp.vue'
import QuizGuid from './GameGuide.vue'
import GamePlay from './GamePlay.vue'
import GameOver from './GameOver.vue'

const views = ref([markRaw(QuizGuid), markRaw(GamePlay), markRaw(GameOver)])

const dataSteps = {
  steps: ['Guide', 'Play', 'Results'],
  currentStep: 1,
  activeColor: '#5182fd',
  passiveColor: '#b3ecff',
};

const StepeProgress = ref(0);
let currentStep = ref(0)

function handelSteps(deriction){
  if(deriction) currentStep.value = StepeProgress.value.netxtStep()
  else currentStep.value = StepeProgress.value.previustStep()
}


</script>

<template>
  <div class="container-fluid">
    <SteperCompe :data="dataSteps" ref="StepeProgress" />

    <main class="flex-grow-1 main">
      <div>
        <component :is="views[currentStep]"/>
      </div>
    </main>
    <div class="fixed-bottom bg-white py-3">
      <div class="container">
        <div class="d-flex justify-content-between">
          <button class="btn btn-info" @click="handelSteps(false)">Previous</button>
          <button class="btn btn-info" @click="handelSteps(true)">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>


<style>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('https://gamethinking.io/wp-content/uploads/sites/5/2018/12/quiz-background-1024x576.png');
  height: calc(100vh - 132px); /* 100vh minus the heights of the header and footer */
}
</style>
