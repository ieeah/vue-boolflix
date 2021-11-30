<template>
	<div id="app">
		<div class="top_header">
			<Header @startSearching="performSearch"/>
		</div>
		<main>
			<Body id="Body"
			:movies="movies"
			:tvShows="tvShows"/>
		</main>
	</div>
</template>

<script>
import Header from '@/components/Header.vue';
import Body from '@/components/Body.vue';
import axios from 'axios';

export default {
	name: 'App',
	components: {
		Header,
		Body,
	},
	data() {
		return {
			moviesToShow: [],
			tvShows: [],
			movies: [],
			BabyK : 'ca6604e774b1404964077082d0e1bb94',
		};
	},
	methods: {
		performSearch(title) {
			let one = "https://api.themoviedb.org/3/search/movie"
			let two = "https://api.themoviedb.org/3/search/tv"
			const requestOne = axios.get(one, {
				params: {
					api_key: this.BabyK,
					query: title,
					language: 'it',
				}
			});
			const requestTwo = axios.get(two, {
				params: {
					api_key: this.BabyK,
					query: title,
					language: 'it',
				}
			});

			axios.all([requestOne, requestTwo])
			.then(axios.spread((...responses) => {
			const responseOne = responses[0]
			const responseTwo = responses[1]
			// use/access the results
			// console.log(responseOne, responseTwo);
			this.movies = [];
			this.tvShows = [];
			this.movies = responseOne.data.results;
			this.tvShows = responseTwo.data.results;
			})).catch(errors => {
			// react on errors.
			console.log(errors);
			})
			this.moviesToShow = [],
			this.moviesToShow.push(...this.movies, ...this.tvShows);
		},
	},
}
</script>

<style lang="scss">
@import '@/styles/globals.scss';
</style>
