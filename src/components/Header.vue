<template>
	<header>
		<a href="/">
			<img
				:src="require('@/assets/CapretteTibetane_logo.svg')"
				alt="Logo di caprette tibetane"
			>
		</a>
		<div class="search-bar">
			<select v-model="selectedLanguage"
					name="selectLanguage" id=""
					@change="$emit('changedLanguage', selectedLanguage)"
			>
				<option value="it">Ita</option>
				<option value="en">Eng</option>
			</select>
			<input type="text" v-model="lookFor" placeholder="Cerca un film" @keyup.enter="$emit('startSearching', lookFor), clearSearchBar()">
			<div
				class="btn"
				@click="$emit('startSearching', lookFor), clearSearchBar()"
			>
				<i class="fas fa-search"></i>
				Search
			</div>
			<div class="reset btn"
				@click="$emit('searchReset')"
			>
				Reset
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
			selectedLanguage: 'it',
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
			width: 45%;
			height: 100%;
			@include flex-center;

			select {
				width: 80px;
				height: 40px;
				border-radius: 10px;
			}
			select,
			input {
				border-radius: 10px;
				color: $secondary-color;
				border: none;
				outline: 2px solid $secondary-color;
				&:hover,
				&:active,
				&:focus {
					outline-offset: 3px;
				}
			}

			select,
			input,
			.btn {
				padding-inline: 10px;
				padding-block: 5px;
				height: 40px;
				font-size: 1.2rem;
			}

			input {
				width: 65%;
				position: relative;
				margin-inline: 20px;
			}

			.btn {
				width: 25%;
				background-color: $secondary-color;
				color: $primary-color;
				cursor: pointer;
				border-radius: 5px;
				@include flex-center;
				i {
					margin-right: 5px;
				}
				&:hover {
					opacity: .6;
				}
				&.reset {
					background-color: rgba($color: $secondary-color, $alpha: .4);
					outline: 1px solid $accent-color;
					color: $secondary-color;
					margin-left: 20px;
					&:hover {
						background-color: rgba($color: $secondary-color, $alpha: .7);
						color: $primary-color;
					}
				}
			}
		}
	}
</style>