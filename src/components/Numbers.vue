<script setup lang="ts">
import { ref, computed } from 'vue';

let limit = ref(100);
const numberList = computed(() => generateNumberList());


function generateNumberList() {
  const numbers = Array.from({ length: limit.value }, (_, index) => index);
  return numbers.sort(() => Math.random() - 0.5);
}


function hov(number) {
  const nums = document.querySelectorAll('.number');

  for(let i = 0; i < nums.length; i++)
  {
    const num = nums[i].textContent.trim();
    if(number % num === 0)
    {
      nums[i].classList.add('active')
      console.log('divisor', num)
    }
  }
}

function reset()
{
	const nums = document.querySelectorAll('.number');
	nums.forEach(num => num.classList.remove('active'))
}
</script>

<template>
	<div class="wrapper">
    <div class="labelInput">
      <label for="limit">Limit</label>
      <input id="limit" type="number" v-model="limit" />
    </div>

    <div class="numberList">
      <div 
        class="number"
        :id="'number-'+number"
        v-for="number in numberList"
        :key="number"
        @mouseover="hov(number)"
        @mouseout="reset"
      >
        {{ number }}
      </div>
    </div>
	</div>
</template>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap:2rem;
}

.labelInput {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.numberList {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.number {
  padding: 0.3125rem;
  display: inline-block;
  background-color: lightgrey;
}

.active {
  background-color: red;
}
</style>
