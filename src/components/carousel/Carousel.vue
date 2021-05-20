<template>
	<div class="carousel">
		<slot></slot>
		<button class="carousel__nav carousel__prev" @click='prev'><i class="fas fa-backward"></i></button>
		<button class="carousel__nav carousel__next" @click='next'><i class="fas fa-forward"></i></button>
		<div class="carousel__pagination">
			<button v-for="n in slidesCount" @click='goTo(n-1)' :class="{active: n - 1 === index}" :key="n"></button>
		</div>
	</div>
</template>
<script>
export default {
	data(){
		return {
			index: 0,
			slides: [],
			direction: 'right'
		}
	},
	watch: {
		slides(slides){
			if (this.index >= this.slidesCount){
				this.index = this.slidesCount - 1
			}
			if (slides.length == 0){
				this.index = 0
			}
		}
	},
	computed : {
		slidesCount() {
			return this.slides.length
		}
	},
	methods:  {
		next(){
			this.index++
			this.direction = 'right'
			if (this.index >= this.slidesCount){
				this.index=0 
			}
		},
		prev(){
			this.index--
			this.direction = 'left'
			if (this.index < 0){
				this.index = this.slidesCount-1
			}
		},
		goTo(index){
			this.direction = index > this.index ? 'right' : 'left'
			this.index = index
		}
	},
	mounted() {
		this.slides = this.$children
	}
}
</script>
<style>
	.carousel {position: relative;width: 630px;margin: auto;overflow: hidden;}
	.carousel__nav{
		color: white;
		border: none;
		background: transparent;
		position: absolute;
		top: 50%;
		font-size: 50px;
		cursor: pointer;
	}
	.carousel__prev{
		left: 10px;
	}
	.carousel__next{
		right: 10px;
	}
	.carousel__pagination{
		position: absolute;
		bottom: 10px;
		left: 0;
		right: 0;
		text-align: center;
	}
	.carousel__pagination button {
		border: none;
		display: inline-block;
		width: 10px;
		height: 10px;
		background-color: black;
		opacity: 0.8;
		border-radius: 10px;
		margin: 0 2px;
	}
	.carousel__pagination button.active {
		background-color: #fff;
	}
</style>