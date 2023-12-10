<script setup>
import { computed, ref } from "vue";
import CalcButton from "./CalcButton.vue";
const number = ref("");
const number2 = ref("");
const calcsign = ref("");
const current = computed(() => {
  return number.value.concat(calcsign.value).concat(number2.value);
});
const display = ref("0");

function clear() {
  number.value = "";
  number2.value = "";
  calcsign.value = "";
  updateDisplay();
}

function sign(val) {
  calcsign.value = val;
  updateDisplay();
}

function equation(val) {
  if (!calcsign.value) {
    number.value = number.value.concat(val);
  } else {
    number2.value = number2.value.concat(val);
  }
  updateDisplay();
}

function calculate() {
  let result;

  switch (calcsign.value) {
    case "+":
      result = parseFloat(number.value) + parseFloat(number2.value);
      break;
    case "-":
      result = parseFloat(number.value) - parseFloat(number2.value);
      break;
    case "*":
      result = parseFloat(number.value) * parseFloat(number2.value);
      break;
    case "/":
      result = parseFloat(number.value) / parseFloat(number2.value);
      break;
    case "%":
      result = (parseFloat(number.value) * parseFloat(number2.value)) / 100;
      break;
    default:
      result = 0;
  }

  display.value = result.toString();

  // Clear the input values for the next calculation
  number.value = "";
  number2.value = "";
  calcsign.value = "";
}

function updateDisplay() {
  // Update the display with the current input values
  display.value = current.value || "0";
}
</script>

<template>
  <div class="flex items-center justify-center">
    <div class="h-full bg-blue-300 mx-auto py-6 px-5 rounded-lg">
      <!-- result section -->
      <div class="bg-white rounded-md h-28 mb-6 flex items-center justify-end">
        <div class="text-6xl pr-3">{{ display || 0 }}</div>
      </div>
      <!-- numbers section -->
      <div class="flex flex-col gap-5">
        <div class="flex gap-3 items-center mx-auto">
          <!-- numbers -->
          <CalcButton @click="clear" class="bg-orange-400">C</CalcButton>
          <CalcButton @click="sign('+')" class="bg-orange-400">+</CalcButton>
          <CalcButton @click="sign('%')" class="bg-orange-400">%</CalcButton>
          <CalcButton @click="sign('/')" class="bg-orange-400">/</CalcButton>
        </div>
        <div class="flex gap-3 items-center mx-auto">
          <CalcButton @click="equation(7)">7</CalcButton>
          <CalcButton @click="equation(8)">8</CalcButton>
          <CalcButton @click="equation(9)">9</CalcButton>
          <CalcButton @click="sign('*')" class="bg-orange-400">*</CalcButton>
        </div>
        <div class="flex gap-3 items-center mx-auto">
          <CalcButton @click="equation(4)">4</CalcButton>
          <CalcButton @click="equation(5)">5</CalcButton>
          <CalcButton @click="equation(6)">6</CalcButton>
          <CalcButton @click="sign('-')" class="bg-orange-400">-</CalcButton>
        </div>
        <div class="flex gap-3 items-center mx-auto">
          <CalcButton @click="equation(1)">1</CalcButton>
          <CalcButton @click="equation(2)">2</CalcButton>
          <CalcButton @click="equation(3)">3</CalcButton>
          <CalcButton @click="equation(0)">0</CalcButton>
        </div>
        <div>
          <CalcButton @click="calculate" class="w-full bg-yellow-300"
            >=</CalcButton
          >
        </div>
      </div>
    </div>
  </div>
</template>
