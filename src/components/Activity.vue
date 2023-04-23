<script setup lang="ts">
import { ref } from "vue";

defineProps({
	name: {
		type: String,
		required: true,
	},
	steps: {
		type: Array,
		required: true,
	},
	points: {
		type: Number || String,
		required: true,
	},
	totalTime: {
		type: Number || String,
		required: true,
	},
	image: {
		type: String,
	},
});

const arrow = ref("▲");
</script>

<template>
	<div :style="{ backgroundImage: `url(${image})`, backgroundSize: 'cover' }">
		<h2>{{ name }}</h2>
		<h3>Time Left: {{ totalTime }}</h3>
		<h3>+{{ points }}</h3>
		<button @click="arrow = arrow === '▼' ? '▲' : '▼'">Steps {{ arrow }}</button>
		<div v-if="arrow === '▼'" v-for="(step, index) in steps" :key="index">{{ index }}. {{ step }}</div>
	</div>
</template>

<style scoped>
button {
	background-color: transparent;
	cursor: pointer;
	border: 1px solid black;
	border-radius: 10px;
	padding: 5px;
}
</style>
