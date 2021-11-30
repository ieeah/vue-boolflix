<template>
	<div class="movie">
		<h2
			v-if="title"
		>
			{{title}}
		</h2>
		<p
			v-show="originalTitle != title"
		>
			{{originalTitle}}
		</p>
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
		<img
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
	},
	data() {
		return {
			flags: ['it', 'en'],
		};
	},
}
</script>

<style scoped lang="scss">
@import '@/styles/globals.scss'

</style>