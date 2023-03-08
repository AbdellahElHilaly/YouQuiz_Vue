<script setup>
  import {defineProps , ref , computed , defineExpose} from 'vue'
  import IconDone from './icons/IconDone.vue'
  const props = defineProps({
    data : Object,
  });
  props.data.currentStep--;
  const data = ref(props.data)
  const cssStyle = computed(() => {
    return {
      '--active-color': data.value.activeColor,
      '--passive-color': data.value.passiveColor,
    };
  })

const testVar = 45;
  function netxtStep(){
    if(data.value.currentStep < data.value.steps.length){
      data.value.currentStep++;
    }
    return data.value.currentStep;
  };

  function previustStep(){
    if(data.value.currentStep > 0){
      data.value.currentStep--;
    }
    return data.value.currentStep;
  };

  defineExpose({
    netxtStep,
    previustStep,
  });



</script>

<template>
  <div class="steps-container" :style="cssStyle">
    <ul class="steps-list">
      <li class="step" v-for="(step, index) in data.steps" :key="index" 
      :class="
        (index == data.currentStep) ? 'step-active' : '' ,
        (index < data.currentStep) ? 'step-done' : '' ,
        (index == 0 && index == data.currentStep) ? 'step-done-in-advance' : '' 
      ">

        <div class="step-bubble">
          <div class="step-count">{{ index + 1}}</div>
          <IconDone/>
        </div>
        <div class="step-label">{{ step}}</div>
        <div class="step-line">
          <div class="line-fill"></div>
        </div>
      </li>
    </ul>
  </div>
</template>


<style scoped>
  .steps-container{
    width: 100%;
    margin: auto;
    margin-bottom: 40px;
    padding-top: 15px;
  }
  .steps-list{
    display: flex;
    list-style: none;
  }
  .step{
    display: flex;
    align-items: center;
    flex-grow: 1;
    max-width: 100%;
    position: relative;
    height: 60px;
  }

  .line-fill{
    width: 0;
    height: 5px;
    background-color: var(--active-color);
    transition: all .3s ease;
  }

  .step:last-child{
    max-width: 60px;
  }

  .step-label{
    font-weight: 500;
    font-size: 18px;
    position: absolute;
    bottom: -30px;
    opacity: .7;
    color: var(--passive-color);
  }

  .step-bubble {
    width: 35px;
    height: 35px;
    border-radius: 50%;
    background-color: var(--passive-color);
    transition: all .3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .step-count{
    color: white;
    font-weight: 500;
    font-size: 20px;
    display: none;
    transition: transform .3s ease;
  }

  .step-done-icon{
    display: none;
  }
  .step-line{
    width: 100%;
    height: 5px;
    background-color: var(--passive-color);
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    z-index: -10;
  }

  .step:last-child .step-line{
    display: none;
  }

  .step-active .step-count {
    display: block;
    transform: scale(1.2); /* Zoom in the step count */
  }

  .step-active .step-bubble {
    width: 60px;
    height: 60px;
    background-color: var(--active-color);
    transform: scale(1.2); /* Zoom in the step bubble */
  }
  .step-done .step-bubble{
    width: 60px;
    height: 60px;
    background-color: var(--active-color);
  }
  .step-done .step-done-icon{
    display: block;
  }
  .step-done .line-fill{
    width: 100%;
  }

  .step-done-in-advance .line-fill{
      width: 50%;
  }

  .step-active .step-label,
  .step-done .step-label{
    opacity: 1;
    color: var(--active-color);
  }

</style>
