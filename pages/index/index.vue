<template>
	<view>
		<view class="content">
			<view></view>
			<view></view>
			<view></view>
			<view></view>
		</view>
		<!-- <ourGoTop :scrollY="1000" /> -->
		<our-go-top></our-go-top>
	</view>
</template>

<script>
	import ourGoTop from '@/components/our-gotop/our-gotop.vue'
	
	export default {
		components: { ourGoTop },
		data() {
			return {
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss">
.content {
	&>view{
		height: 100vh;
		&:nth-of-type(1) {
			background-color: $uni-color-primary;
		}	
		&:nth-of-type(2) {
			background-color: $uni-color-success;
		}	
		&:nth-of-type(3) {
			background-color: $uni-color-warning;
		}	
		&:nth-of-type(4) {
			background-color: $uni-color-error;
		}
		
	}
}	
</style>
