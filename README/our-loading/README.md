# Our-Loading

这是一款基于适用于**H5**和**微信小程序端**的自定义加载中组件😀😀😀
---
## 注意

本组件只在微信小程序和H5端测试过，如有问题请指正

## 预览

这里的内部样式需要你自己去改我的源码，我有标记好了，就是换个**loader**，其实就是改个组件就行，**默认为`shrinkRect`**

> 原因是uni-app不支持动态组件，如果以后支持，我就修改为自动配置不需要改源码

| shrinkRect                                                   | loop                                                         | bounce                                                       | doubleBounce                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/shrinkRect.gif) | ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/loop.gif>) | ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/bounce.gif>) | ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/doubleBounce.gif>) |

| doubleCube                                                   | doubleDot                                                    | rotatePlane                                                  | scaleOut                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/doubleCube.gif>) | ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/doubleDot.gif>) | ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/rotatePlane.gif>) | ![](<https://gitee.com/Owlism/owlComponents/raw/master/README/our-loading/scaleOut.gif>) |

## 使用步骤

### 引入

```javascript
import ourLoading from '@/components/our-loading/our-loading.vue'

export default {
	components: { ourLoading }
}
```

### 使用

#### 例子1：在某元素内使用
需要为那个元素设置宽高，并且相对定位
```html
<template>
  <div class='parent'>
    <ourLoading active text="loading..." />
  </div>
</template>
<style scoped>
    .parent {
        position: relative;  /* 注意需要为加载器定义一个相对定位的父容器 */
    }
</style>
```
#### 例子2：全屏使用

```html
<template>
  <div>
     <!--isFullScreen 可以实其全屏显示-->
    <ourLoading isFullScreen active text="loading..." />
  </div>
</template>
```

#### 例子3：自定义加载动画

```html
<template>
  <div class='parent'>
      <our-loading active >
          <img  src="../static/loader.gif" />
      </our-loading>
  </div>
</template>
<style scoped>
    .parent {
        position: relative;  /* 注意需要为加载器定义一个相对定位的父容器 */
    }
</style>
```

### 可配参数

| 参数          | 类型  | 默认值              | 单位            | 描述                                                |
| ---------------- | ------- | ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| active           | Boolean | false                   |                    | 控制是否显示                                                 |
| translateY | Number | 150            | %                | 加载图型样式向上移动多少自身的距离，如输入**50**则垂直居中 |
| color            | String  | #333                 |                     | 加载的内置图型样式的颜色以及字体颜色                            |
| background-color | String  | rgba(255, 255, 255, .9) |  | 加载蒙板的背景色                                             |
| size             | Number  | 40                    | px                 | 加载的内置图型样式的大小（对自定义的加载图型无效）（**注意这里并非准确40px的大小，因为我内部做了些调整，大多数情况下，不需要改这个值**） |
| isFullScreen   | Boolean | false                   |                    | 控制加载动画是否全屏展示                                     |
| text             | String  |                         |                         | 自定义文本，显示在加载图标下方                               |

