<template>
  <transition name="fade">
    <view
      v-show="isShow"
      @click="goTop"
      :style="{
        width: `${width}px`,
        height: `${height}px`,
        right: `${right}px`,
        bottom: `${bottom}px`,
        zIndex: zIndex
      }"
      class="gotop">
        <slot>
          <view>
            <svg t="1587113576016" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="2222" :width="width" :height="height">
              <path :fill="color" d="M523.955 297.952l323.744 512c6.24 9.856 6.624 22.336 0.992 32.512-5.632 10.24-16.384 16.576-28.033 16.576l-647.328 0c-11.647 0-22.4-6.336-28.033-16.576-2.656-4.8-3.968-10.112-3.968-15.424 0-5.952 1.664-11.904 4.929-17.088l323.616-512c5.856-9.28 16.064-14.911 27.04-14.912s21.184 5.632 27.04 14.912z" p-id="2223"></path>
            </svg>
          </view>
        </slot>
      </view>
    </view>
  </transition>
</template>

<script>
export default {
  name: 'ourGoTop',
  data () {
    return {
      timer: null,
      isShow: false
    }
  },
  props: {
    width: {
      type: Number,
      default: 50
    },
    height: {
      type: Number,
      default: 50
    },
		
    right: {
      type: Number,
      default: 30
    },
    bottom: {
      type: Number,
      default: 50
    },
    zIndex: {
      type: Number,
      default: 1000
    },
    color: {
      type: String,
      default: '#333'
    },
    scrollY: {
      type: Number,
      default: 1000
    },
    scrollSpeed: {
      type: Number,
      default: 100
    },
		duration: {
			type: Number,
			default: 300
		}
  },
  mounted () {
		//#ifndef H5
		this.isShow = true
		//#endif
		
		//#ifdef  H5
			window.addEventListener('scroll', this.scrollAnimate)
		//#endif
  },
  beforeDestroy () {
		//#ifdef H5
      window.removeEventListener('scroll', this.scrollAnimate)
		//#endif
  },
  methods: {
		//#ifndef H5
			goTop () {
				uni.pageScrollTo({
					scrollTop: 0,
					duration: this.duration
				});
			}
		//#endif
		
		//#ifdef H5
			scrollAnimate () {
				if (window.scrollY >= this.scrollY && this.isShow === false) {
					this.isShow = true
				} else if (window.scrollY < this.scrollY && this.isShow === true) {
					this.isShow = false
				}
			},
			goTop () {
				let self = this
				if (self.timer) {
					cancelAnimationFrame(self.timer);
				}
				self.timer = requestAnimationFrame(function fn(){
					let oTop = document.body.scrollTop || document.documentElement.scrollTop;
					if(oTop > 0){
						document.body.scrollTop = document.documentElement.scrollTop = oTop - self.scrollSpeed;
						self.timer = requestAnimationFrame(fn);
					}else{
						cancelAnimationFrame(self.timer);
					}
				})
			}
		//#endif
  }
}
</script>

<style scoped>
.gotop {
	position: fixed;
	display: flex;
	justify-content: center;
	align-items: center;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-to,
.fade-leave {
  opacity: 1;
}

.fade-enter-active,
.fade-leave-active {
  transition: 0.5s all linear
}
</style>
