# Vuejs

## 渐进式概念

对于引入新框架的项目，可将一部分页面用新框架代码替换旧框架代码，循序渐进地替换并不起冲突。（新框架可兼容于旧框架使用）



## Vue的加载使用

1、CDN（分为开发环境及生产环境）开发环境适用于开发阶段调试

用语句将vuejs从服务器连接

2、下载引入

直接下载至本地通过script导入

3、NPM安装（实际项目使用）



## 响应式概念

当数据发生改变时（赋值更新），在页面直接显示更新后的状态。



## MVVM模式在vue的实现

model（数据层）：plain JavaScript object（定义对象）

view（视图）：DOM（实际可以看到的界面）

view model（DOM listener、data bindings）：	Vue（实现监听及绑定）



## Vue Options

创建VUE实例可添加的属性，如下，

el：接收css选择器字符串或element，选定作用的节点；

data：接收对象或函数（在组件模式下为函数），将对象内的变量通过引用加载到DOM内

methods：接收函数

```vue
<div id="app">
    {{massage}}
</div>
<script src="../js/vue.js"></script>//载入vue
let app = new Vue({
	el: "#app",
	data: {
		massage = "print",
		age = "20"
}，
	methods: {
		sayhi: function(){
			console.log("hi"),
}
}
})
```

### tip方法与函数的区别

直接定义的称为函数；构造函数内定义，通过实例调用的函数称为方法。



## Vue的生命周期

指vue或组件自创建开始至销毁的全过程。在生命周期中，有接口可传入函数（beforecreate、created、beforemount、mounted、beforeupdate、updated、beforedestroy、destroyed）。当定义函数后，会在不同阶段回调应用函数。



### tip前端缩进方式

缩进两个空格

