<template>
	<div>
		<div class="banner" v-on:click="handleBannerClick">
			<img class="banner-img" :src="bannerImg" />
			<div class="banner-info">
				<div class="banner-title">{{ this.sightName }}</div>
				<div class="banner-number">
					<span class="iconfont banner-icon">&#xe61b;</span>
					{{ this.bannerImgs.length }}
				</div>
			</div>
		</div>
		<fade-animation>
			<common-gallary :imgs="bannerImgs" v-show="showGallary" v-on:close="handleGallaryClose"></common-gallary>
		</fade-animation>
	</div>
</template>

<script>
	import CommonGallary from 'common/gallary/Gallary'
	import FadeAnimation from 'common/fade/FadeAnimation'
	export default {
		name: 'DetailBanner',
		components: {
			CommonGallary,
			FadeAnimation
		},
		props: {
			sightName: String,
			bannerImg: String,
			bannerImgs: Array
		},
		data() {
			return {
				showGallary: false
			}
		},
		methods: {
			handleBannerClick() {
				this.showGallary = true
			},
			handleGallaryClose() {
				this.showGallary = false
			}
		}
	}
</script>

<style lang="stylus" scoped>
	.banner
		overflow: hidden
		height: 0
		padding-bottom: 55%
		position: relative
		.banner-img
			width: 100%
		.banner-info
			display: flex
			position: absolute
			left: 0
			right: 0
			bottom: 0
			line-height: .6rem
			color: #fff
			background-image: linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,.8))
			.banner-title
				flex: 1
				font-size: .32rem
				padding: 0 .2rem
			.banner-number
				margin-top: .18rem
				padding: 0 .4rem
				height: .32rem
				line-height: .32rem
				border-radius: .2rem
				background: rgba(0,0,0,.8)
				font-size: .24rem
				.banner-icon
					font-size: .24rem
</style>