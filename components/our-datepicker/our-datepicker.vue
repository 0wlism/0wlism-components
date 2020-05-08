<template>
	<view>
		<view class="our-date-picker-wrapper">
		    <view class="our-date-picker-header" :style="{ backgroundColor:color }">
		      <view class="our-date-picker-btn our-date-picker-btn-pre" @click="preMonth">pre</view>
		      <view>{{this.thisYear}}-{{this.thisMonth}}</view>
		      <view class="our-date-picker-btn our-date-picker-btn-next" @click="nextMonth">next</view>
		    </view>
		    <view class="our-date-picker-body">
		      <view class="our-date-picker-body-table">
		        <view class="our-date-picker-body-table-header">
							<view>一</view>
							<view>二</view>
							<view>三</view>
							<view>四</view>
							<view>五</view>
							<view>六</view>
							<view>日</view>
		        </view>
		        <view class="our-date-picker-body-table-body" @click="emitDate($event)">
							<view
								hover-class="hover-cell" 
								:class="{ thisMonth: item.month === thisMonth }" :style="{ color: item.month === thisMonth? color: '#a1a1a1' }"
								v-for="item in monthData" :key="item.date"
								:data-date="item.date" :data-month="item.month">{{ item.showDate }}</view>
		        </view>
		      </view>
		    </view>
		  </view>
	</view>
</template>

<script>
	export default {
		name: 'ourDatePicker',
		props: {
			year: {
				type: Number,
				default: new Date().getFullYear()
			},
			month: {
				type: Number,
				default: new Date().getMonth() + 1
			},
			color: {
				type: String,
				default: '#333'
			}
		},
		data() {
			return {
				lastDateOfLastMonth: -1, // 上个月的最后一天
				lastDateOfThisMonth: -1, // 这个月的最后一天
				thisYear: this.year,
				thisMonth: this.month,
				monthData: []
			}
		},
		watch: {
			thisYear(newv) {
				this.getMonthData(newv, this.thisMonth)
			},
 			thisMonth(newv) {
				this.getMonthData(this.thisYear, newv)
			}
		},
		mounted() {
			this.getMonthData(this.year, this.month)
		},
		methods: {
			// 向外发送日期数据
			emitDate(e) {
				let date = Number(e.target.dataset.date)
				let month = Number(e.target.dataset.month)
				let year = this.thisYear
				// 如果是上个月
				if (date <= 0) {
					date += this.lastDateOfLastMonth
					if(month === 12) {
						year -= 1
					}
				}
				// 如果是下个月
				else if (date > this.lastDateOfThisMonth) {
					date -= this.lastDateOfThisMonth
					if(month === 1) {
						year += 1
					}
				}
				this.$emit('clickToGetDate', {
					month,
					date,
					year,
					dateObj: new Date(year, month, date)
				})
			},
			preMonth() {
				if((this.thisMonth - 1) <= 0) {
					this.thisMonth =  12
					this.thisYear -= 1
				} else {
					this.thisMonth -= 1
				}
			},
			nextMonth() {
				if((this.thisMonth + 1) >= 13) {
					this.thisMonth =  1
					this.thisYear += 1
				} else {
					this.thisMonth += 1					
				}
			},
			getMonthData(year, month) {
				if (!year || !month) {
					year = year || new Date().getFullYear()
					month = (month && ((month <= 12 && month >= 0 ) && month)) || new Date().getMonth() + 1
				}
				// 当月的第一天
				let firstDateOfThisMonth = new Date(year, month-1, 1)
				// 当月的第一天的星期数
				let dayOffirstDateOfThisMonth = firstDateOfThisMonth.getDay()
				if (dayOffirstDateOfThisMonth === 0) {
					dayOffirstDateOfThisMonth = 7
				}
				// 上个月的最后一天
				this.lastDateOfLastMonth = new Date(year, month-1, 0).getDate()
				// 上个月有几天
				let lastMonthDayCount = dayOffirstDateOfThisMonth - 1
				// 当月的最后一天
				// 这里把它存到data是为了方便后续的事件委托
				this.lastDateOfThisMonth = new Date(year, month, 0).getDate()
				
				// 直接遍历日历（假设6周）
				this.monthData = []
				for (let i = 0; i < 7 * 6; i++) {
					let date = i + 1 - lastMonthDayCount // 日期，但是上个月的日期为负数，下个月的日期不是以1开始
					let showDate = date  // 正常显示的日期
					let thisMonth = month // 当前月份
					// 如果是上个月
					if (date <= 0) {
						thisMonth = month - 1
						showDate = this.lastDateOfLastMonth + date
					}
					// 如果是下个月
					else if (date > this.lastDateOfThisMonth) {
						thisMonth = month + 1
						showDate = date - this.lastDateOfThisMonth
					}
					if (thisMonth === 0) {
						thisMonth = 12
					} else if (thisMonth === 13) {
						thisMonth = 1
					}
					this.monthData.push({
						month: thisMonth,
						date: date,
						showDate: showDate
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
@mixin table-cell {
	text-align: center;
	height: calc(100vw / 7);
	line-height: calc(100vw / 7);
	border: 1px solid #f8f8f8;
	font-size: 28rpx;
}	

.our-date-picker-wrapper {
		position: fixed;
		bottom: 0;
    overflow: hidden;
    width: 100vw;
    box-shadow: 2px 2px 10px 2px rgba(128, 128, 128, .3);
		border-top-left-radius: 20rpx;
		border-top-right-radius: 20rpx;
		.our-date-picker-header {
			display: flex;
			justify-content: space-between;
			height: 100rpx;
			line-height: 100rpx;
			border-bottom: 1px solid #f8f8f8;
			color: #fff;
			.our-date-picker-btn {
				width: 100rpx;
				height: 100rpx;
				font-family: serif;
				font-size: 40rpx;
				text-align: center;
				line-height: 100rpx;
			}
		}
		.our-date-picker-body-table {
			.our-date-picker-body-table-header {
				display: grid;
				grid-template-columns: repeat(7, minmax(0, 1fr));
				&>view {
					@include table-cell;
					border: none;
					font-size: 30rpx;
					font-weight: 600;
				}
			}
			.our-date-picker-body-table-body {
				display: grid;
				grid-template-columns: repeat(7, minmax(0, 1fr));
				&>view {
					@include table-cell
					&.thisMonth {
						text-shadow: 1px 1px 1px rgba(0,0,0,.3);
					}
					&.hover-cell {
						background-color: darken($color: #fff, $amount: 5%);
					}
				}
			}
		}
}
</style>
