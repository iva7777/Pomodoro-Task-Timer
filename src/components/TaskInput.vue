<template>
    <form @submit.prevent="submitTask">
        <input v-model="task" type="text" placeholder="Enter Your Task">
        <button type="submit">Add Task</button>
    </form>
</template>

<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["add-task"]);
const task = ref("");

const submitTask = () => {
    if (task.value.trim()) {
        emit("add-task", task.value.trim());
        task.value = "";
    }
};

</script>

<style scoped>
form {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    margin: 20px 0;
}

input {
    padding: 12px 16px;
    color: #af1c65;
    border: 2px solid #ff758c;
    border-radius: 10px;
    font-size: 16px;
    outline: none;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    transition: border-color 0.3s, box-shadow 0.3s;
}

input:focus {
    border-color: #ff7eb3;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

button {
    padding: 12px 24px;
    font-size: 16px;
    color: #741343;
    background: linear-gradient(135deg, #ff758c, #f3d2e89e);
    border: none;
    border-radius: 10px;
    cursor: pointer;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    transition: transform 0.2s, box-shadow 0.3s;
}

button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3);
}

button:active {
    transform: translateY(1px);
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}
</style>