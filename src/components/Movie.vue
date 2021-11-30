<template>
	<div class="movie">
		<h2>{{title}} {{name}}</h2>
		<p
			v-if="!flags.includes(originalLanguage)"
		>
			{{originalLanguage}}
		</p>
		<img v-else
			class="flag" alt=""
			:src="require(`@/assets/flags/${originalLanguage}.png`)"
		>
		<p>{{voteAverage}}</p>
		<img v-if="posterPath!= null"
			:src="`https://image.tmdb.org/t/p/w185${posterPath}`"
			:alt="title">
	</div>
</template>

<script>
export default {
	name: 'Movie',
	props: {
		title: String,
		originalTitle: String,
		originalLanguage: String,
		voteAverage: Number,
		posterPath: String,
		name: String,
	},
	data() {
		return {
			flags: ['it', 'en'],
		};
	},
}
</script>

<style scoped lang="scss">
@import '@/styles/globals.scss';

.flag {
	width: 50px;
	height: 30px;
}
</style>