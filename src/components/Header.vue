<template>
	<header>
		<a href="/">
			<h1>boolflix</h1>
		</a>
		<div class="search-bar">
			<input type="text" v-model="lookFor" @keyup.enter="$emit('startSearching', lookFor), clearSearchBar()">
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
		justify-content: space-between;
		align-items: center;
		background-color: $secondary-color;
		height: 72px;
		padding: $fsz-7;

		a {
			text-decoration: none;
		}
		.search-bar {
			width: 30%;
			height: 100%;
			@include flex-center;
			
			input,
			.btn {
				padding-inline: 10px;
				padding-block: 5px;
				border-radius: 80px;
			}

			input {
				width: 65%;
				border: none;
				outline: none;
				position: relative;
				&:hover,
				&:active,
				&:focus {
					border: none;
					outline: 2px solid $accent-color;
					outline-offset: 2px;
				}
			}

			.btn {
				width: 25%;
				background-color: $accent-color;
				color: $secondary-color;
				margin-left: 20px;
				cursor: pointer;
				@include flex-center;
				i {
					margin-right: 5px;
				}
			}
		}
	}
</style>