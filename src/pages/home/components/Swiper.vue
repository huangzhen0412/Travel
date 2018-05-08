<template>
	<swiper :options="swiperOption">
    	<!-- slides -->
    	<swiper-slide v-for="item of swiperList" :key="item.id">
    		<img class="swiper-img" :src="item.imgUrl">
    	</swiper-slide>
    	<!-- Optional controls -->
    	<div class="swiper-pagination"  slot="pagination"></div>
  	</swiper>
</template>

<script>
	export default {
		name: 'HomeSwiper',
		data() {
			return {
				swiperOption: {
					pagination: '.swiper-pagination'
				},
				swiperList: [
					{
						id: 1,
						imgUrl: 'https://img1.qunarzz.com/qs/1805/66/29a40eeb420e0302.jpg'
					},
					{
						id: 2,
						imgUrl: 'https://img1.qunarzz.com/qs/1805/a9/f01d076cea2ee902.jpg'
					}
				]
			}
		}
	}
</script>

<style lang="stylus" scoped>
	>>> .swiper-pagination-bullet-active
		background: #fff
	.swiper-img
		width: 100%
</style>