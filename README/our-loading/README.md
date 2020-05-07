# Our-Loading

这是一款基于适用于**H5**和**微信小程序端**的自定义加载中组件😀😀😀
---
## 注意

本组件只在微信小程序和H5端测试过，如有问题请指正

## 预览

这里的内部样式需要你自己去改我的源码，我有标记好了，就是换个**loader**，其实就是改个组件就行，**默认为`shrinkRect`**

> 原因是uni-app和微信小程序不支持动态组件，如果以后支持，我就修改为自动配置不需要改源码

| shrinkRect                                                   | loop                                                         | bounce                                                       | doubleBounce                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/shrinkRect.gif) | ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/loop.gif) | ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/bounce.gif) | ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/doubleBounce.gif) |

| doubleCube                                                   | doubleDot                                                    | rotatePlane                                                  | scaleOut                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/doubleCube.gif) | ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/doubleDot.gif) | ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/rotatePlane.gif) | ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/scaleOut.gif) |

## 使用步骤

### 引入
#### 全局引入（推荐）
在`main.js`里引入
```javascript
// ......
import ourLoading from '@/components/our-loading/our-loading.vue'
Vue.component('ourLoading', ourLoading)
// ......
```
全局引入之后，直接在任何地方使用

#### 局部引入

```javascript
import ourLoading from '@/components/our-loading/our-loading.vue'

export default {
	components: { ourLoading }
}
```

### 使用

#### 例子1：全屏使用（推荐）

```html
<template>
  <div>
     <!--isFullScreen 可以实其全屏显示-->
    <ourLoading isFullScreen active text="loading..." />
  </div>
</template>
```
#### 例子2：在某元素内使用
需要为那个元素设置宽高，并且设置为相对定位
```html
<template>
  <div class='parent'>
    <ourLoading active text="loading..." />
  </div>
</template>
<style scoped>
    .parent {
        width: 100vw;
        height: 50vh;
        position: relative;  /* 注意需要为加载器定义一个相对定位的父容器 */
    }
</style>
```
#### 例子3：自定义加载动画

```html
<template>
	<view>
		<view class="parent">
			<our-loading active text="加载中...">
				<image class="img" src="../../static/loading.gif" mode="aspectFit" />
			</our-loading>
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
```

效果如下：

|                        自定义加载动画                        |
| :----------------------------------------------------------: |
| ![](D:\Program\0wlism-components\README\our-loading\diyloading.gif) |





### 可配参数

| 参数          | 类型  | 默认值              | 单位            | 描述                                                |
| ---------------- | ------- | ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| active           | Boolean | false                   |                    | 控制是否显示                                                 |
| translateY | Number | 150            | %                | 加载图型样式向上移动多少自身的距离，如输入**50**则垂直居中 |
| color            | String  | #333                 |                     | 加载的内置图型样式的颜色                            |
| textColor | String | #333 | | 加载字体的颜色 |
| background-color | String  | rgba(255, 255, 255, .9) |  | 加载蒙板的背景色                                             |
| size             | Number  | 40                    | px                 | 加载的内置图型样式的大小（对自定义的加载图型无效）（**注意这里并非准确40px的大小，因为我内部做了些调整，大多数情况下，不需要改这个值**） |
| isFullScreen   | Boolean | false                   |                    | 控制加载动画是否全屏展示                                     |
| text             | String  |                         |                         | 自定义文本，显示在加载图标下方                               |

