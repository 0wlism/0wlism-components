

## 预览
![](https://gitee.com/Owlism/owlComponents/raw/master/README/0wlism-gotop/show.gif)

## 注意

本组件只在微信小程序和H5端测试过，如有问题请指正

## 使用步骤

### 引入
```javascript
import ourGoTop from '@/components/our-gotop/our-gotop.vue'

export default {
	components: { ourGoTop }
}
```
### 使用

H5端可以这样

```html
<template>
	<view>
		<view>
			<view></view>
			<view></view>
			<view></view>
			<view></view>
		</view>
		<!-- 在页面里使用，默认为内置图标 -->
		<ourGoTop />
	</view>
</template>
```
也可以自定义自己的内容（**小程序端只能自定义自己的内容，只能用这种方式**）

```html
<template>
	<view>
		<view>
			<view></view>
			<view></view>
			<view></view>
			<view></view>
		</view>
		<!-- 在页面里使用，用自己定义的内容 -->
		<our-go-top>
			<view>TOP</view>
		</our-go-top>
	</view>
</template>
```
## 可配置属性

| 参数       |  类型   | 默认值 | 描述                                                 | 注意（没说明的都行） |
| ----------- | ------ | ------- | ----------------------------------------------------------- | ----------- |
| scrollY     | Number | 1000    | 控制滚动到距离视口上方多少显示组件，如果设置为0，则永久显示 | 这个属性在H5端才有用，在小程序端组件永久显示 |
| scrollSpeed | Number | 100     | 滚动到上方的速度                                            | 这个值在H5才有效 |
| duration | Number | 300 | 滚动的动画时间 | 这个值在小程序端才有效 |
| color       | String | #333    | 内置图标的颜色                                              | 这个属性在H5端才有用 |
| right       | Number | 30      | 距离视口右边的距离                                          |  |
| bottom      | Number | 50      | 距离视口下边的距离                                          |  |
| width       | Number | 50      | 图标的宽度                                                  |  |
| height      | Number | 50      | 图标的高度                                                  |  |
| zIndex      | Number | 1000    | 层级                                                        |  |
