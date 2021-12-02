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
				<div class="cta">
					<a v-if="title || name"
						:href="`https://www.youtube.com/results?search_query=${title}+trailer+${selectedLanguage}`"
						target="_blank"
					>
						<i class="fab fa-youtube"></i>
					</a>
					
				</div>
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
		selectedLanguage: String,
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
		transform-style: preserve-3d;
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
			display: flex;
			flex-direction: column;
			position: absolute;
			top: 0;
			left: 0;
			padding: 20px;
			background-color: rgba($color: black, $alpha: .9);
			opacity: 0;
			transition: transform .5s ease-in-out;
			overflow: hidden;
			&:hover {
				opacity: 1;
			}
			h2 {
				font-size: $fsz-5;
				color: $primary-color;
				margin-bottom: 10px;
			}
			.rating {
				color: $secondary-color;
			}
			p {
				font-size: $fsz-6;
				margin-top: 10px;
				flex-grow: 1;
				text-overflow: ellipsis;
				white-space: nowrap;
				overflow: hidden;
				padding-right: $fsz-7;
				&::-webkit-scrollbar {
					background-color: transparent;
					border-radius: 20px;/* roundness of the scroll thumb */
					border: 0;
				}
				&::-webkit-scrollbar-thumb {
					background-color: rgba($color: $secondary-color, $alpha: 0.7);
					border-radius: 100px;
					width: .5em;
				}

				@supports (scrollbar-color: red blue) {
					* {
						scrollbar-color: rgba(255, 255, 255, .2) $secondary-color; 
						scrollbar-width: thin;
					}
				}
			}
			.cta {
				width: calc(100% - 25px);
				justify-self: end;
				display: flex;
				align-items: center;
				justify-content: space-between;
				margin-top: 10px;
				a {
					color: $youtube-red;
				}
			}
		}
	}
}
</style>