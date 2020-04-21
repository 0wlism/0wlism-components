<template>
	<view>
		<view class="content">
			<view></view>
			<view></view>
			<view></view>
			<view></view>
		</view>
		<!-- <owlismGoTop :scrollY="1000" /> -->
		<owlism-go-top>
			<view>TOP</view>
		</owlism-go-top>
	</view>
</template>

<script>
	import owlismGoTop from '@/components/0wlism-gotop/0wlism-gotop.vue'
	
	export default {
		components: { owlismGoTop },
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
