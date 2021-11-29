<template>
	<div class="container-full">
		<div class="movie" v-for="movie in movies2" :key="`${movie.title}`">
			<h1>{{movie.title}}</h1>
			<p>{{movie.actor}}</p>
			<p>{{movie.year}}</p>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Body',
	data() {
		return {
			movies2: [
				{
				title: 'ciaone',
				year: '1999',
				actor: 'robert downey jr',
				},
				{
				title: 'filippa',
				year: '2010',
				actor: 'pietreppaolo',
				},
			],
		};
	},
	props: {
		movies: Array,
	},
}
</script>

<style scoped lang="scss">

</style>