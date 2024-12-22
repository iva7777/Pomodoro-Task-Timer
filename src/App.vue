<script setup lang="ts">
import { ref } from "vue";
import TimerDisplay from "./components/TimerDisplay.vue";
import ControlButton from "./components/ControlButton.vue";
import TaskInput from "./components/TaskInput.vue";

const time = ref(25 * 60);
const isRunning = ref(false);
const task = ref<string | null>(null);
const isTaskCompleted = ref(false);
let timer: NodeJS.Timeout | null = null;

const startTimer = () => {
  if (!isRunning.value) {
    isRunning.value = true;
    timer = setInterval(() => {
      if (time.value > 0) {
        time.value--;
      } else {
        resetTimer();
        alert("Time's up!");
      }
    }, 1000);
  }
};

const pauseTimer = () => {
  isRunning.value = false;
  if (timer) clearInterval(timer);
};

const resetTimer = () => {
  isRunning.value = false;
  time.value = 25 * 60;
  if (timer) clearInterval(timer);
};

const addTask = (newTask: string) => {
  task.value = newTask;
  isTaskCompleted.value = false;
};

const toggleTaskCompletion = () => {
  isTaskCompleted.value = !isTaskCompleted.value;
};
</script>

<template>
  <div class="app-container">
    <h1>Pomodoro Timer</h1>
    <TaskInput @add-task="addTask" />
    <TimerDisplay :time="time" />
    <ControlButton :isRunning="isRunning" @start="startTimer" @pause="pauseTimer" @reset="resetTimer" />
    <div v-if="task" class="current-task" @click="toggleTaskCompletion">
      <strong :class="{ completed: isTaskCompleted }">Current Task: {{ task }}</strong>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  position: relative;
  text-align: center;
  max-width: 600px;
  margin: 0;
  font-family: 'Segoe UI';
}

h1 {
  font-size: 48px;
  margin-bottom: 20px;
}

.current-task {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px 0;
  padding: 10px;
  background-color: #f2d4d4;
  border: 2px solid #ff758c;
  border-radius: 10px;
  cursor: pointer;
  user-select: none;
}

.completed {
  text-decoration: line-through;
  opacity: 0.5;
  background: #faced3;
  box-shadow: none;
}
</style>
