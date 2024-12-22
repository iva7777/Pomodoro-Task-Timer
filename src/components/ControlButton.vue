<template>
    <div class="control-buttons">
        <button @click="$emit('start')" :disabled="isRunning">Start</button>
        <button @click="$emit('pause')" :disabled="!isRunning">Pause</button>
        <button @click="$emit('reset')">Reset</button>
    </div>
</template>

<script setup lang="ts">
const props = defineProps<{
    isRunning: boolean;
}>();
</script>

<style scoped>
button {
    margin: 5px;
    padding: 12px 24px;
    font-size: 16px;
    color: #333;
    background: linear-gradient(135deg, #f3bcd0, #ff758c);
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

button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    background: #faced3;
    box-shadow: none;
}
</style>