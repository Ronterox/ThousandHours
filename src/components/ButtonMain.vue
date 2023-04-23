<script setup lang="ts">
import { ref } from "vue";
import JSConfetti from "js-confetti";

const props = defineProps({
	goal: {
		type: Number,
		required: true,
	},
});

const count = ref(0);
const estimatedTime = ref(0);
const timeStart = ref(new Date().getTime() / 1000);

const countdownInterval = ref<number | null>(null);
const countdownIntervalTimeStart = ref(timeStart.value);
const countdown = ref(0);

const penaltyInterval = ref<number | null>(null);

setInterval(() => {
	if (countdownInterval.value || penaltyInterval.value || countdownIntervalTimeStart.value !== timeStart.value) 
	{
		countdownIntervalTimeStart.value = timeStart.value;
		return;
	}
	countdown.value = 5;
	countdownInterval.value = setInterval(() => {
		if (countdown.value === 0) {
			clearInterval(countdownInterval.value!);
			countdownInterval.value = null;
			penaltyInterval.value = setInterval(() => {
				count.value -= Math.ceil(props.goal * 0.005);
			}, 1000);
		} else countdown.value--;
	}, 1000);
}, 5000);

function handleClick() {
	count.value++;
	if (count.value === props.goal) new JSConfetti().addConfetti();

	if (countdownInterval.value) {
		clearInterval(countdownInterval.value);
		countdownInterval.value = null;
	}
	if (penaltyInterval.value)
	{
		clearInterval(penaltyInterval.value);
		penaltyInterval.value = null;
	}
	if (count.value % 3 !== 0) return;

	const timeEnd = new Date().getTime() / 1000;
	estimatedTime.value = (timeEnd - timeStart.value) * (props.goal - count.value);
	timeStart.value = timeEnd;
}
</script>

<template>
	<p>Time Left: {{ Math.round((estimatedTime / 3600) % 24) }}:{{ Math.round((estimatedTime / 60) % 60) }}:{{ Math.round(estimatedTime % 60) }}</p>
	<button @click="handleClick">{{ count }} / {{ goal }}</button>
	<h2>{{ countdown }} secs</h2>
</template>

<style scoped>
button {
	background-color: #42b983;
	color: white;
	font-size: 1.5em;
	margin: 1em;
	padding: 0.25em 1em;
	border: 2px solid #42b983;
	border-radius: 3px;
}

button:hover {
	background-color: #3d8b6d;
	border-color: #3d8b6d;
	cursor: pointer;
}
</style>
