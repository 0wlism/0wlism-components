<template>
	<view>
		<view class="parent">
			<our-loading color="red" textColor="red" active text="加载中..." />
			<!-- <our-loading active text="加载中...">
				<image class="img" src="../../static/loading.gif" mode="aspectFit" />
			</our-loading> -->
		</view>
	</view>
</template>

<script>
	import ourLoading from '@/components/our-loading/our-loading.vue'
	
	export default {
		components: { ourLoading }
	}
</script>

<style lang="scss">
.parent {
	width: 100vw;
	height: 100vh;
	position: relative;  /* 注意需要为加载器定义一个相对定位的父容器 */
	.img {
		max-width: 30vw;
		height: 100rpx;
	}
}
</style>
