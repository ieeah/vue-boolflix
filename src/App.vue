<template>
	<div id="app">
		<div class="top_header">
			<Header @startSearching="performSearch"
					@searchReset="resetSearch"
					@changedLanguage="setLanguage"/>
		</div>
		<main>
			<Body id="Body"
			:movies="movies"
			:tvShows="tvShows"
			:selectedLanguage="selectedLanguage"/>
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
			searchIsOff: true,
			selectedLanguage: 'it',
		};
	},
	methods: {
		performSearch(title) {
			this.query = title;
			this.searchIsOff = false;
			let one = "https://api.themoviedb.org/3/search/movie"
			let two = "https://api.themoviedb.org/3/search/tv"
			const requestOne = axios.get(one, {
				params: {
					api_key: this.BabyK,
					query: title,
					language: this.selectedLanguage,
				}
			});
			const requestTwo = axios.get(two, {
				params: {
					api_key: this.BabyK,
					query: title,
					language: this.selectedLanguage,
				}
			});

			axios.all([requestOne, requestTwo])
			.then(axios.spread((...responses) => {
			const responseOne = responses[0]
			const responseTwo = responses[1]
			this.movies = [];
			this.tvShows = [];
			this.movies = responseOne.data.results;
			this.tvShows = responseTwo.data.results;
			})).catch(errors => {
			console.log(errors);
			})
			this.moviesToShow = [],
			this.moviesToShow.push(...this.movies, ...this.tvShows);
		},
		resetSearch() {
			this.movies = [];
			this.moviesToShow = [];
			this.tvShows = [];
		},
		setLanguage(lang) {
			this.selectedLanguage = lang;
		},
	},
}
</script>

<style lang="scss">
@import '@/styles/globals.scss';
</style>
