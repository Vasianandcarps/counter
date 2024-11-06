<script setup lang="ts">
import { ref } from 'vue';

// Масив для зберігання прізвищ і дат прийому на роботу
const employees = ref([
  { surname: '', hireDate: '' },
  { surname: '', hireDate: '' },
  { surname: '', hireDate: '' },
  { surname: '', hireDate: '' },
  { surname: '', hireDate: '' }
]);

// Функція для розрахунку середнього стажу
const calculateAverageExperience = () => {
  const currentDate = new Date();
  let totalYears = 0;
  let count = 0;

  employees.value.forEach(employee => {
    if (employee.hireDate) {
      const hireDate = new Date(employee.hireDate);
      const experienceYears = currentDate.getFullYear() - hireDate.getFullYear();
      totalYears += experienceYears;
      count++;
    }
  });

  return count > 0 ? Math.floor(totalYears / count) : 0;
};

// Результат середнього стажу
const averageExperience = ref<number | null>(null);

// Функція, яка викликається при натисканні кнопки
const onCountExperience = () => {
  averageExperience.value = calculateAverageExperience();
};
</script>

<template>
  <div id="counter">
    <div v-for="(employee, index) in employees" :key="index" class="worker">
      <input type="text" v-model="employee.surname" placeholder="Прізвище" />
      <input type="date" v-model="employee.hireDate" />
    </div>
    <button @click="onCountExperience">Count experience</button>
    <div v-if="averageExperience !== null" class="result">
      Середній стаж роботи: {{ averageExperience }} років
    </div>
  </div>
</template>

<style scoped>
* {
  text-align: center;
}
#counter {
  width: 400px;
  height: 550px;
  border-radius: 50px;
  margin: auto;
  background: #1d0f0f;
  color: white;
  padding: 20px;
  margin-top: 150px;
}
.worker input {
  margin-top: 20px;
  display: block;
  width: 80%;
  margin-left: auto;
  margin-right: auto;
}

button {
  background: #e49f0a;
  color: white;
  border-radius: 10px;
  padding: 10px 15px;
  margin-top: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

button:disabled {
  background: #706d67;
  border: 0px;
  cursor: not-allowed;
}

button:hover {
  transform: scale(1.1) translateY(5px);
}

input {
  background: transparent;
  border: 0;
  border-bottom: 2px solid #7b7c81;
  color: white;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
.result {
  margin-top: 20px;
  font-size: 18px;
}
</style>