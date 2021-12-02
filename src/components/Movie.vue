<template>
	<div class="movie">
		<h2>{{title}} {{name}}</h2>
		<p
			v-if="!flags.includes(originalLanguage)"
		>
			{{originalLanguage}}
		</p>
		<img v-else
			class="flag" :alt="title || name"
			:src="require(`@/assets/flags/${originalLanguage}.png`)"
		>
		<div class="rating">
			<span v-for="(element, i) in Math.ceil(voteAverage / 2)"
				:key="`rating${i}`"
			>
				<i class="fas fa-star"></i>
			</span>
			<span v-for="(element, i) in 5 - (Math.ceil(voteAverage / 2))"
				:key="`emptyRating${i}`"
			>
				<i class="far fa-star"></i>
			</span>
		</div>
		<img v-if="posterPath"
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
.movie {
	width: calc(100% / 3);
	height: 400px;
	background-color: red;
}

.flag {
	width: 50px;
	height: 30px;
}

.rating {
	display: flex;
	align-items: center;
	color: $accent-color;
	font-size: .8rem;
}
</style>