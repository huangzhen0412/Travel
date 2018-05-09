<template>
	<div>
		<home-header></home-header>
		<home-swiper :list="swiperList"></home-swiper>
		<home-icons :icon="iconList"></home-icons>
		<home-recommend :recommend="recommendList"></home-recommend>
		<home-weekend :weekend="weekendList"></home-weekend>
	</div>
</template>

<script>
	import HomeHeader from './components/Header'
	import HomeSwiper from './components/Swiper'
	import HomeIcons from './components/Icons'
	import HomeRecommend from './components/Recommend'
	import HomeWeekend from './components/Weekend'

	import axios from 'axios'

	import { mapState } from 'vuex'

	export default {
		name: 'Home',
		components: {
			HomeHeader,
			HomeSwiper,
			HomeIcons,
			HomeRecommend,
			HomeWeekend
		},
		data() {
			return {
				// city: '',
				swiperList: [],
				iconList: [],
				recommendList: [],
				weekendList: [],
				lastCity: ''
			}
		},
		computed: {
			...mapState(['city'])
		},
		mounted: function() {
			this.lastCity = this.city
			this.getHomeInfo()
		},
		activated: function() {
			if(this.lastCity !== this.city){
				this.lastCity = this.city
				this.getHomeInfo()
			}
		},
		methods: {
			getHomeInfo() {
				axios.get('/api/index.json?city=' + this.city)
					.then(this.getHomeInfoSucc)
			},
			getHomeInfoSucc(res) {
				res = res.data
				if(res.ret && res.data) {
					const data = res.data
					// this.city = data.city
					this.swiperList = data.swiperList
					this.iconList = data.iconList
					this.recommendList = data.recommendList
					this.weekendList = data.weekendList
				}
			}
		}
	}
</script>

<style>
	
</style>