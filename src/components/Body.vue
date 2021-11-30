<template>
	<div class="container-full">


		<div v-if="moviesToShow.length == 0" class="loader">
			<h2>Sono pronto a cercare il tuo film!</h2>
			<div class="loading_animation">
				<div class="ani1">cerca il film</div>
				<div class="ani2">o la serie</div>
			</div>
		</div>


		<div v-else class="movies_list">
			<Movie class="movie"
				v-for="movie in moviesToShow"
				:key="`${movie.id}`"
				:title="movie.title"
				:originalTitle="movie.original_title"
				:originalLanguage="movie.original_language"
				:voteAverage="movie.vote_average"
				:posterPath="movie.poster_path"
				:name="movie.name"
			/>
		</div>


	</div>
</template>

<script>
import Movie from '@/components/Movie.vue';
export default {
	name: 'Body',
	components: {
		Movie,
	},
	props: {
		movies: Array,
		tvShows: Array,
	},
	computed: {
		moviesToShow() {
			const lista = [];
			lista.push(...this.movies, ...this.tvShows);
			// lista.forEach(element => {
			// 	if (element.name != '' || element.name != undefined) {
			// 		element.title = element.name;
			// 	}
			// });
			return lista ;
		},
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
		font-size: 2rem;
	}
	50% {
		width: 0;
		height: 0;
		border-radius: 0;
		filter: brightness(100%) opacity(.2);
		font-size: 0rem;
	}
	100% {
		width: 50px;
		height: 50px;
		border-radius: 50%;
		background-color: $accent-color;
		filter: brightness(80%) opacity(1);
		font-size: 2rem;
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
			animation: 4s ease-in-out infinite scaleup alternate ;
		}
		.ani2 {
			animation: 4s ease-in-out infinite scaleup alternate ;
			animation-delay: 2s;
		}
	}
</style>