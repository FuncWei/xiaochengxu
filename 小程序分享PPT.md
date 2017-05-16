title: 微信小程序
speaker: 魏广洪
url: https://github.com/FuncWei/xiaochengxu
transition: slide2
files: /js/demo.js,/css/demo.css
theme:moon

[slide]

# 微信小程序分享
<!-- ## 演讲者：魏广洪 -->

[slide]
# CONTENTS 
----
1. 小程序介绍
2. 小程序框架
3. view视图层
4. appServer逻辑层

[slide]

# 小程序介绍

[slide]

# 小程序是什么 {:&.flexbox.vleft}

小程序是一种不需要下载、安装即可使用的应用，它实现了触手可及的梦想，用户扫一扫或者搜一下即开打开应用，也实现了用完即走的理念，用户不用关心安装太多应用的问题。


[slide]

# 实现技术区别 
----
* 公众号基于H5，小程序基于微信自身开发环境与开发语言 
	* <p class="text-success" style="font-size: 16px;margin-bottom: 20px;"> {:&.rollIn}
	小程序是微信内的云端应用（所以无需安装），不是原生App，通过WebSocket双向通信（保证无需刷新即时通信）、本地缓存（图片与UI 本地缓存降低与服务器交互延时）以及微信底层技术优化，相当于架在原有系统中的新的操作系统，小程序借助微信与系统间交互，使得能够拥有原生APP 的体验。而这一点恰巧是HTML5 web 应用的不足，导致其主要用于业务逻辑与交互简单的应用中。</p> 

	* <p class="text-white" style="font-size: 16px;margin-bottom: 20px;">
	公众号是基于传统H5开发与运行，传统H5运行环境是浏览器，以公众号菜单栏内嵌H5页面的形式，完成了基础功能的微信化植入，但通常都是比较简单的页面，操作体验比较一般。
	</p>

	* <p class="text-success" style="font-size: 16px;margin-bottom: 20px;">
	微信小程序运行环境并非完整的浏览器，开发过程中用到H5相关的技术。微信小程序的运行环境是微信基于浏览器内核完全重构的一个内置解析器，针对小程序专门做了优化，配合自己定义的开发语言标准WXML、WXSS、UI组件（基于H5 进行了优化），提升了小程序的性能。
	</p>	


[slide]

# 体验上的差别
----
* 公众号操作延时较大，小程序体验接近原生App
	* <p class="text-info" style="font-size: 16px;margin-bottom: 20px;"> {:&.rollIn}
	公众号中点击应用功能后顶部出现绿色进度需要等一段时间，对于业务逻辑复杂交互要求高的应用使用起来体验较差。而小程序将会非常流畅几乎无需等待，类似普通APP操作一样流畅。主要原因是公众号没有本地缓存，所以每次打开都是会请求服务器刷新页面，造成延时较长体验下降，小程序对UI 与图片本地缓存，只需要对服务器请求交互数据，页面切换无需刷新</p>

	* <p class="text-warning" style="font-size: 16px;margin-bottom: 20px;">
	最大的亮点在于微信提供了丰富的框架组件和API接口供开发者调用，具体包含：界面、视图、内容、按钮、导航、多媒体、位置、数据、网络、重力感应等。在这些组件和接口的帮助下，建立在微信上的小程序在运行能力和流畅度上面便可以保持和Native APP一样的体验。
	</p>

[slide]

[magic data-transition="earthquake"]
# 小程序的优势
----
* <span>无需安装、随用随点</span>
* <span>类WEB、不是HTML5</span>
* <span>基于微信跨平台</span>
* <span>丰富的组件和API</span>

========

# 小程序的缺点
----
* <span>客户端计算能力不及APP</span>
* <span>不支持第三方插件</span>
[/magic]

[slide]

# 小程序框架

[slide]

	> 1.小程序的框架命名MINA，意思是MINA IS NOT APP。MINA的核心是一个响应的数据绑定系统,整个系统分为两块：视图层(View) 和 逻辑层(App Service)。

	> 2.MINA管理了整个小程序的页面路由，可以做到页面间的无缝切换，并给以页面完整的生命周期。

	> 3.MINA提供了一套基础的(具有微信风格和微信逻辑的)组件，开发者通过组合各种基础组件，创建自己的微信小程序。

	> 4.MINA提供丰富的微信原生API，调用微信功能十分方便（自个儿家产的当然用着方便），如获取用户信息，本地存储，支付功能等。

	<div class="columns2" style="margin-top: 20px;">
		<img src="/img/mina.png" style=" height:250px;">
		<img src="/img/jiagou.png" style="height:250px;">
	</div>
[slide]

## 小程序架构

	<img src="/img/jiagou1.png">


[slide]

## 小程序加载

	<img src="/img/jiazai.png">


[slide]
# view视图层
#### 视图层由 WXML 与 WXSS 编写，由组件来进行展示。

[slide]

<h2 style="text-align: left;">WXML</h2>

<p style="font-size: 18px;margin-bottom: 20px;text-align: left;">
	WXML：(WeiXin Markup Language)是MINA设计的一套标签语言，结合基础组件、事件系统，可以构建出页面的结构。与HTML类似，WXML也采用了声明式结构，具体作用和HTML一样构造页面结构。不过从变现形式来看WXML更加类似于XML。
</p>

* <span class="label label-primary">支持数据绑定</span>
* <span class="label label-warning">支持逻辑算术、运算</span>
* <span class="label label-danger">支持模板、引用</span>
* <span class="label label-default">支持添加事件（bindtap）</span>
<img src="/img/wxml.png" style="margin-top: 20px;">


[slide]

<h2 style="text-align: left;">WXSS</h2>

<p style="font-size: 18px;margin-bottom: 20px;text-align: left;">
	WXSS：(WeiXin Style Sheets)是MINA设计的一套样式语言，用于描述WXML的组件样式。WXSS类似于CSS，都是用来控制页面元素的样式。微信官方称WXSS具备CSS的大部分特性，这点和React Native以及Weex一样，都是CSS的子集，但是具备哪些CSS特性官方并没有公布。除此之外，WXSS还引入了样式单位这个概念。
</p>

* <span class="label label-primary">支持大部分CSS特性</span>
* <span class="label label-warning">添加尺寸单位rpx(responsive pixel 响应像素),可根据屏幕宽度自适应</span>
* <span class="label label-danger">使用@import语句可以导入外联样式表</span>
* <span class="label label-default">不支持多层选择器-避免被组件内结构破坏</span>
<img src="/img/wcss.png" style="margin-top: 20px;">

[slide]
<h2>UI组件</h2>
<img src="/img/zujian.png">

[slide]
# appServer逻辑层
#### 逻辑层将数据进行处理后发送给视图层，同时接受视图层的事件反馈。

[slide]

<h2 style="text-align: left;">注册程序-App()</h2>
<p style="font-size: 18px;margin-bottom: 20px;text-align: left;">
	App() 函数用来注册一个小程序。接受一个 object 参数，其指定小程序的生命周期函数等。App( ) 是小程序的入口，相当于main函数。
</p>
<pre>
	<code class="javascript" style="font-size: 16px;">
		App({
		  onLaunch: function(options) { 
		  // 监听小程序初始化  当小程序初始化完成时，会触发 onLaunch（全局只触发一次).
		     
		  },
		  onShow: function(options) {
		  // 监听小程序显示  当小程序启动，或从后台进入前台显示，会触发 onShow.
		     
		  }, 
		  onHide: function() {
		  // 监听小程序隐藏  当小程序从前台进入后台，会触发 onHide.
		     
		  },
		  onError: function(msg) {
		  // 错误监听函数  当小程序发生脚本错误，或者 api 调用失败时，会触发 onError 并带上错误信息
		    console.log(msg)
		  },
		  globalData: 'I am global data'
		})
	</code>
</pre>
[slide]

<h2 style="text-align: left;">注册页面-Page()</h2>
<p style="font-size: 18px;margin-bottom: 20px;text-align: left;">
	Page() 函数用来注册一个页面。接受一个 object 参数，其指定页面的初始数据、生命周期函数、事件处理函数等。
</p>

<pre>
	<code class="javascript" style="font-size: 16px;max-height: 400px;">
Page({
  data: {
  	// 页面的初始数据
    text: "This is page data."
  },
  onLoad: function(options) {
  	// 监听页面加载

  },
  onShow: function() {
   	// 监听页面显示

  },
  onReady: function() {
  	// 监听页面初次渲染完成

  },
  onHide: function() {
    // 监听页面隐藏

  },
  onUnload: function() {
    // 监听页面卸载

  },
  onPullDownRefresh: function() {
    // 监听用户下拉动作

  },
  onReachBottom: function() {
    // 页面上拉触底事件的处理函数

  },
  onShareAppMessage: function () {
   // 用户点击右上角分享

  },
  // Event handler.
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    })
  },
  customData: {
    hi: 'MINA'
  }
})
	</code>
</pre>

[slide]

##生命周期
<img src="/img/zouqi.png">

[slide]
<h2 style="text-align: left;">页面路由</h2>

<p style="font-size: 18px;margin-bottom: 20px;text-align: left;">
	在小程序中所有页面的路由全部由框架进行管理，框架以栈的形式维护了当前的所有页面。
</p>

<img src="/img/luyou.png">

[slide]
# THANK YOU



