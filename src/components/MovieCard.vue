<template>
	<div class="movie">
		<div class="card_content">
			<div class="card_img">
				<img v-if="posterPath" :src="`https://image.tmdb.org/t/p/w185${posterPath}`"
				alt="title">
				<img v-else src="../assets/ncv.jpg" alt="" class="centered_image">
			</div>
			<div class="movie_details">
				<h2>{{title}} {{name}}</h2>
				<div class="rating">
						<span v-for="(element, i) in Math.ceil(voteAverage / 2)"
							:key="`rating${i}`"
						>
							<i class="fas fa-star"></i>
						</span>
						<span v-for="(element, i) in 5 - (Math.ceil(voteAverage / 2))"
							:key="`emptyRating${i}`"
						>
							<i class="far fa-star"></i>
						</span>
				</div>
				<p>{{overview}}</p>
			</div>
		</div>
		
	</div>
</template>

<script>
export default {
	name: 'MovieCard',
	props: {
		posterPath: String,
		title: String,
		name: String,
		voteAverage: Number,
		overview: String,
	},
}
</script>

<style scoped lang="scss">
@import '@/styles/globals.scss';
.movie {
	width: calc((100% - 100px) / 5);
	height: 420px;
	flex-shrink: 0;
	margin: 0 10px 20px 10px;
	cursor: pointer;
	.card_content {
		@include _100;
		position: relative;
		.card_img {
			@include _100;
			img {
				@include _100;
				object-fit: cover;
				object-position: top center;
			}
			.centered_image {
				object-position: center;
			}
		}
		.movie_details {
			@include _100;
			position: absolute;
			top: 0;
			left: 0;
			backdrop-filter: blur(10px);
			padding: 20px;
			background-color: rgba($color: black, $alpha: .7);
			opacity: 0;
			transition: all .2s ease-in-out;
			&:hover {
				opacity: 1;
			}
			h2 {
				font-size: $fsz-5;
				color: $primary-color;
			}
			.rating {
				color: $secondary-color;
			}
			p {
				font-size: $fsz-6;
			}
		}
	}
}
</style>