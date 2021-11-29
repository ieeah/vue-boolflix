<template>
	<div id="app">
		<div class="top_header">
			<Header @startSearching="performSearch"/>
		</div>
		<main>
			<Body id="Body"/>
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
			lookFor: '',
		};
	},
	methods: {
		performSearch(title) {
			axios.get('https://api.themoviedb.org/3/search/movie', {
				params: {
					api_key: 'ca6604e774b1404964077082d0e1bb94',
					query: title,
				}
			})
			.then(function (response) {
				console.log(response.data);
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
