<template>
    <div class="timer-display">
        <span>{{ minutes }}</span>:<span>{{ seconds }}</span>
    </div>
</template>

<script setup lang="ts">
import { computed } from "vue";
const props = defineProps<{
    time: number;
}>();

const minutes = computed(() => Math.floor(props.time / 60).toString().padStart(2, "0"));
const seconds = computed(() => (props.time % 60).toString().padStart(2, "0"));


</script>

<style scoped>
.timer-display {
    display: inline-block;
    background: linear-gradient(135deg, #ff7eb3, #ff758c);
    color: #fff;
    font-size: 3rem;
    font-weight: bold;
    padding: 20px 40px;
    border-radius: 20px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
    text-align: center;
    width: fit-content;
    margin: 40px;
}

.time {
    font-family: "Courier New", Courier, monospace;
}
</style>