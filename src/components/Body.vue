<template>
	<div class="container-full">
		<div class="movie" v-for="movie in movies" :key="`${movie.title}`">
			<h2>{{movie.title}}</h2>
			<p>{{movie.original_title}}</p>
			<p v-if="!flags.includes(movie.original_language)">{{ movie.original_language}}</p>
			<img v-else :src="require(`@/assets/flags/${movie.original_language}.png`)" alt="">
			<p>{{movie.vote_average}}</p>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Body',
	props: {
		movies: Array,
	},
	data() {
		return {
			flags: ['it', 'en'],
		};
	},
}
</script>

<style scoped lang="scss">
	.movie {
		img {
			width: 50px;
			height: 30px;
		}
	}
</style>