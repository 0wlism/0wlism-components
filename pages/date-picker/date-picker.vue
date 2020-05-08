<template>
	<view>
		<our-date-picker @clickToGetDate="getDate"></our-date-picker>
	</view>
</template>

<script>
	import ourDatePicker from '@/components/our-datepicker/our-datepicker.vue'
	
	export default {
		components: { ourDatePicker },
		data() {
			return {
				
			};
		},
		methods:{
			getDate(obj) {
				console.log(obj)
			}
		}
	}
</script>

<style lang="scss">

</style>
