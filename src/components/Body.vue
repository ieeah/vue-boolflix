<template>
	<div class="container-full">

		<div class="hero">
			<h2>
				Le caprette tibetane guardano ottimi film, <br>
				sii una capretta anche tu e scegli il tuo!
			</h2>
		</div>
		<div v-if="moviesToShow.length == 0" class="loader">
			<h2>Sono pronto a cercare il tuo film!</h2>
			<div class="loading_animation">
				<div class="ani1">cerca il film</div>
				<div class="ani2">o la serie</div>
			</div>
		</div>


		<div v-else class="cards">
			<h2>Ecco quello che abbiamo trovato per te!</h2>
			<Movie
			v-for="movie in moviesToShow"
			:key="`${movie.id}`"
			:title="movie.title"
			:originalTitle="movie.original_title"
			:originalLanguage="movie.original_language"
			:voteAverage="movie.vote_average"
			:posterPath="movie.poster_path"
			:name="movie.name"
			:overview="movie.overview"
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

.hero {
	width: 100%;
	min-height: 400px;
	padding: 80px;
	background-image: url("../assets/Caprette Tibetane/Hero/HeroSenzaScritte_Caprette-01.svg");
	background-size: cover;
	background-repeat: no-repeat;
	background-position: center;
	display: flex;
	align-items: center;
	h2 {
		width: 35%;
		color: $primary-color;
	}
}

	.loader {
		display: flex;
		align-items: center;
		width: 100%;
		padding: 80px;
		color: $secondary-color;
		h2 {
			width: 20%;
			justify-self: start;
		}
		.loading_animation {
			@include flex-center;
			width: 80%;
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



.cards {
	display: flex;
	flex-wrap: wrap;
	perspective: 1000px;
	padding-inline: $fsz-6;
	h2 {
		width: 100%;
		color: $secondary-color;
		font-weight: 400;
		margin-block: 20px;
		padding-left: 10px;
	}
}
</style>