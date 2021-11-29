<template>
	<div class="container-full">
		<div v-if="movies.length == 0" class="loader">
			<h2>Sono pronto a cercare il tuo film!</h2>
			<div class="loading_animation">
				<div class="ani1"></div>
				<div class="ani2"></div>
			</div>
		</div>
		<div v-else class="movies_list">
			<div class="movie" v-for="movie in movies" :key="`${movie.title}`">
				<h2>{{movie.title}}</h2>
				<p>{{movie.original_title}}</p>
				<p v-if="!flags.includes(movie.original_language)">{{ movie.original_language}}</p>
				<img v-else :src="require(`@/assets/flags/${movie.original_language}.png`)" alt="">
				<p>{{movie.vote_average}}</p>
			</div>
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
@import '@/styles/globals.scss';
@keyframes scaleup {
	0% {
		width: 50px;
		height: 50px;
		border-radius: 50%;
		background-color: $accent-color;
		filter: brightness(80%) opacity(1);
	}
	50% {
		width: 0;
		height: 0;
		border-radius: 0;
		filter: brightness(100%) opacity(.2);
	}
	100% {
		width: 50px;
		height: 50px;
		border-radius: 50%;
		background-color: $accent-color;
		filter: brightness(80%) opacity(1);
	}
}

	.container_full {
		@include flex-center;
		height: calc(100vh - 72px);
	}

	.loader {
		width: 100%;
		height: calc(100vh - 72px);
		@include flex-center;
		h2 {
			width: 20%;
			padding-inline: auto;
		}
		.loading_animation {
			@include flex-center;
			width: 50%;
		}
		.ani1,
		.ani2 {
			margin-inline: 10px;
		}
		.ani1 {
			animation: 2s ease-in-out infinite scaleup alternate ;
		}
		.ani2 {
			animation: 2s ease-in-out infinite scaleup alternate ;
			animation-delay: .5s;
		}
	}
	.movie {
		img {
			width: 50px;
			height: 30px;
		}
	}
</style>