<template>
	<swiper :options="swiperOption" v-if="showSwiper">
    	<swiper-slide v-for="item of list" :key="item.id">
    		<img class="swiper-img" :src="item.imgUrl">
    	</swiper-slide>
    	<div class="swiper-pagination"  slot="pagination"></div>
  	</swiper>
</template>

<script>
	export default {
		name: 'HomeSwiper',
		props: {
			list: Array
		},
		data() {
			return {
				swiperOption: {
					pagination: '.swiper-pagination'
				}
			}
		},
		computed: {
			showSwiper() {
				return this.list.length
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