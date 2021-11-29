<template>
	<div id="app">
		<div class="top_header">
			<Header @startSearching="performSearch"/>
		</div>
		<main>
			<Body id="Body"/>
			<!-- :movies="moviesToShow" -->
		</main>
	</div>
</template>

<script>
import Header from '@/components/Header.vue'
import Body from '@/components/Body.vue'
import axios from'axios'

export default {
	name: 'App',
	components: {
		Header,
		Body,
	},
	data() {
		return {
			moviesToShow: [],
		};
	},
	methods: {
		performSearch(title) {
			axios.get('https://api.themoviedb.org/3/search/movie', {
				params: {
					api_key: 'ca6604e774b1404964077082d0e1bb94',
					query: title,
					language: 'it',
				},
			})
			.then(function (response) {
				// this.moviesToShow.push(response.data.results);
				console.log(this.moviesToShow);
				console.log(response.data.results);
			})
			.catch(function (error) {
				// handle error
				console.log(error);
			})
		},
	},
}
</script>

<style lang="scss">
@import '@/styles/globals.scss';
</style>
