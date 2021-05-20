<template>
	<div>
		<h1>Carousel</h1>
		<Carousel>
			<carousel-slide v-for='n in slides' :key="n" :index='n-1 '>
				<div class="carousel__text">
					Slide {{n}}
				</div>
				<img :src="'https://picsum.photos/id/' + n + '/630/300'" alt="" class="carousel__img">
			</carousel-slide>
		</Carousel>
		<div class="buttons">
			<button @click='addSlide' class="buttons__button">add Slide</button>
			<button @click='removeSlide' class="buttons__button">remove Slide</button>	
		</div>
	</div>
</template>
<script>
	import Carousel from './components/carousel/Carousel'
	import CarouselSlide from './components/carousel/CarouselSlide'
	export default {
		data(){
			return {
				slides: 1
			}
		},
		components: {
			Carousel,
			CarouselSlide
		},
		methods : {
			addSlide(){
				this.slides++
			},
			removeSlide(){
				this.slides--
			}
		}
	}
</script>
<style>
	* {
		padding: 0;
		margin: 0;
		font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
	}
	body {
		background: black;
		overflow: hidden;
	}
	h1 {
		color: white;
		text-align: center;
		margin: 24px 0;
	}
	.carousel__text {
		position: absolute;
		left: 0;
		right: 0;
		text-align: center;
		top: 50%;
		color: white;
		z-index: 999;
	}
	.carousel__img {
		opacity: 0.8;
	}
	.buttons {
		margin-top: 8px;
		text-align: center;
	}
	.buttons__button{
		border: none;
		padding: 10px 15px;
		text-transform: uppercase;
		cursor: pointer;
		transition: all .3s ease-in-out;
	}
	.buttons__button:hover {
		color: white;
		background-color: black;
	}
</style>
