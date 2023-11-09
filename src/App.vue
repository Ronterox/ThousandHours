<script setup lang="ts">
import ButtonMain from "./components/ButtonMain.vue";
import Activity from "./components/Activity.vue";

const IMAGES = {
	study: "https://th.bing.com/th/id/R.df55339b7c7e458e3c4869a82f0aee8c?rik=%2bo%2fKQqA9I9gx9Q&pid=ImgRaw&r=0",
	devlog: "https://th.bing.com/th/id/OIP.YxJ1GtHFXKPmeHkJ51sbeQHaJ4?pid=ImgDet&rs=1",
	meditation: "https://thumbs.dreamstime.com/z/third-eye-concept-meditation-vision-energy-aura-third-eye-concept-meditation-vision-energy-aura-vector-sketch-171184993.jpg",
	nap: "https://th.bing.com/th/id/R.f84debda0a41492b9fd402bafd118b4e?rik=5VjMzBlvL0vG9Q&pid=ImgRaw&r=0",
};

// Show approximated time saving for points
</script>

<template>
	<div id="activities">
		<Activity :image="IMAGES.study" name="Study" :steps="['Select a time', 'Study', 'Complete']" :points="2000" :totalTime="3600" />
		<Activity :image="IMAGES.devlog" name="Devlog" :steps="['Select a time', 'Devlog', 'Complete']" :points="1000" :totalTime="3600" />
		<Activity :image="IMAGES.meditation" name="Meditation" :steps="['Select a time', 'Meditate', 'Complete']" :points="500" :totalTime="3600" />
		<Activity :image="IMAGES.nap" name="Nap" :steps="['Select a time', 'Nap', 'Complete']" :points="700" :totalTime="3600" />
	</div>
	<ButtonMain :goal="10_000" />
	<div id="activities">
		<Activity name="Shower" :steps="['Do it']" :points="300" :totalTime="3600" />
		<Activity name="Upgrade Tool" :steps="['Do it']" :points="800" :totalTime="3600" />
		<Activity name="Create Tool" :steps="['Do it']" :points="900" :totalTime="3600" />
		<Activity name="Sudden Task" :steps="['???']" points="???" totalTime="???" />
	</div>
</template>

<style scoped>
#activities {
	display: flex;
	justify-content: space-around;
	background-color: aliceblue;
}
#activities > div {
	width: 20%;
	padding: 1rem;
	margin: 1rem;
	border: 10px solid black;
	border-radius: 10px;
}
</style>
