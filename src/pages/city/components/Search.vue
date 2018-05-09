<template>
	<div>
		<div class="search">
			<input type="text" placeholder="输入城市名或拼音" class="search-input" v-model="keyword">
		</div>
		<div class="search-content" ref="search" v-show="keyword">
			<ul>
				<li class="search-item border-bottom" v-for="item of list" :key="item.id" v-on:click="handleCityClick(item.name)">{{ item.name }}</li>
				<li class="search-item border-bottom" v-show="hasNoData">没有找到匹配数据</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import Bscroll from 'better-scroll'
	import { mapMutations } from 'vuex'
	export default {
		name: 'CitySearch',
		props: {
			cities: Object
		},
		data() {
			return {
				keyword: '',
				list: [],
				timer: null
			}
		},
		computed: {
			hasNoData() {
				return !this.list.length
			}
		},
		watch: {
			keyword() {
				if(this.timer){
					clearTimeout(this.timer)
				}
				this.timer = setTimeout( () => {
					const result = []
					for(let i in this.cities){
						this.cities[i].forEach((value) => {
							if(value.spell.includes(this.keyword) || value.name.includes(this.keyword)){
								result.push(value)
							}
						})
					}
					this.list = result
					if(!this.keyword){
						this.list = []
					}
				}, 100)
			}
		},
		mounted() {
			this.scroll = new Bscroll(this.$refs.search)
		},
		methods: {
			handleCityClick(city) {
				// this.$store.commit('changeCity', city)
				this.changeCity(city)
				this.$router.push('/')
			},
			...mapMutations(['changeCity'])
		}
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.search
		height: .72rem
		background: $bgColor
		padding: 0 .1rem
		.search-input
			height: .6rem
			line-height: .6rem
			width: 100%
			text-align: center
			border-radius: .06rem
			color: #666
			padding: 0 .1rem
			box-sizing: border-box
	.search-content
		position: absolute
		top: 1.58rem
		left: 0
		right: 0
		bottom: 0
		overflow: hidden
		z-index: 5
		background: #eee
		.search-item
			line-height: .62rem
			padding-left: .2rem
			color: #666
			background: #fff
</style>