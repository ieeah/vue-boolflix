<template>
	<header>
		<a href="/">
			<img
				:src="require('@/assets/CapretteTibetane_logo.svg')"
				alt="Logo di caprette tibetane"
			>
		</a>
		<div class="search-bar">
			<input type="text" v-model="lookFor" placeholder="Cerca un film" @keyup.enter="$emit('startSearching', lookFor), clearSearchBar()">
			<div class="btn" @click="$emit('startSearching', lookFor), clearSearchBar()">
				<i class="fas fa-search"></i>
				Search
			</div>
		</div>
	</header>
</template>

<script>
export default {
	name: 'Header',
	data() {
		return {
			lookFor: '',
		};
	},
	methods: {
		clearSearchBar() {
			this.lookFor = '';
		},
	},
}
</script>

<style scoped lang="scss">
@import '@/styles/globals.scss';
header {
		display: flex;
		width: 100vw;
		justify-content: space-between;
		align-items: center;
		background-color: $primary-color;
		height: 72px;
		padding: $fsz-6;
		position: fixed;
		top: 0;
		left: 0;
		z-index: 1;

		a {
			text-decoration: none;
			display: flex;
			align-items: center;
			img {
				fill: $secondary-color;
			}
		}
		.search-bar {
			width: 30%;
			height: 100%;
			@include flex-center;
			
			input,
			.btn {
				padding-inline: 10px;
				padding-block: 5px;
				height: 40px;
				font-size: 1.2rem;
			}

			input {
				width: 65%;
				border: none;
				outline: 2px solid $secondary-color;
				position: relative;
				border-radius: 10px;
				color: $secondary-color;
				&:hover,
				&:active,
				&:focus {
					border: none;
					outline-offset: 3px;
				}
			}

			.btn {
				width: 25%;
				background-color: $secondary-color;
				color: $primary-color;
				margin-left: 20px;
				cursor: pointer;
				border-radius: 5px;
				@include flex-center;
				i {
					margin-right: 5px;
				}
			}
		}
	}
</style>