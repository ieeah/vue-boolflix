<template>
	<div class="movie">
		<div class="card_content">
			<div class="front_card">
				<img v-if="posterPath"
					:src="`https://image.tmdb.org/t/p/w185${posterPath}`"
					:alt="title"
				>
				<img v-else src="../assets/ncv.jpg"
					alt="no image cover is available"
				>
			</div>
			<div class="back_card">
				<img v-if="posterPath"
					:src="`https://image.tmdb.org/t/p/w185${posterPath}`"
					:alt="title"
				>
				<img v-else src="../assets/ncv.jpg"
					alt="no image cover is available"
				>

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
	</div>
</template>

<script>
export default {
	name: 'Movie',
	props: {
		title: String,
		originalTitle: String,
		originalLanguage: String,
		voteAverage: Number,
		posterPath: String,
		name: String,
		overview: String,
	},
	data() {
		return {
			flags: ['it', 'en'],
		};
	},
}
</script>

<style scoped lang="scss">
@import '@/styles/globals.scss';
.movie {
	width: calc((100% - 100px) / 5);
	margin-inline: 10px;
	margin-bottom: 20px;
	flex-shrink: 0;
	height: 350px;
	cursor: pointer;
	&:hover .card_content {
		transform: rotatey(180deg);
	}
	.card_content {
		transition: transform .4s ease-in-out;
		transform-style: preserve-3d;
		width: 100%;
		height: 100%;
		z-index: 0;
		overflow: hidden;

		.front_card{
		position: absolute;
		width: 100%;
		height: 100%;
		-webkit-backface-visibility: hidden;
		backface-visibility: hidden;
		}

		.front_card {
			img {
				width: 100%;
				height: 100%;
				object-fit: cover;
				object-position: center;
			}
		}

		.back_card {
			img {
				width: 100%;
				height: 100%;
				object-fit: cover;
				object-position: center;
				filter: blur(10px);
			}

			.movie_details {
				position: absolute;
				left: 0;
				top: 0;
				width: 100%;
				height: 100%;
				padding: 20px;
				background-color: rgba(0,0,0, .8);

				h2 {
					font-size: 1.5rem;
					color: $primary-color;
					margin-bottom: 20px;
				}

				.rating {
					color: $secondary-color;
				}

				p {
					margin-top: 20px;
					font-size: .8rem;
				}
			}
		}
	}
}

.flag {
	width: 50px;
	height: 30px;
}

.rating {
	display: flex;
	align-items: center;
	color: $accent-color;
	font-size: .8rem;
}
</style>