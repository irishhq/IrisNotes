## 概述
- 小程序wxml 是一种xml文件用于描述网页结构
xml-格式要求非常严格
	- 一个xml文件必须有且只有一个根元素
	- 所有标签有开始必须有结束
	- 属性值必须双引号
- 组件
- rpx和设计稿一致，font-size用px
- js程序
	1. ECMAScript
		基本数据类型：number;string;boolean;null;undefined;
		引入				:	Object;Number;Date;RegExp;
	2. 小程序没有BOM/DOM概念（document,window,alert()）
	3. 小程序顶级对象`wx` 
## 生命周期
生命周期:一个组件从创建到销毁过程
### 全局生命周期:app.js
- onLaunch 当小程序运行只执行一次

### 局部生命周期(组件生命周期)
- 1.`onLoad` 组件加载时触发一个组件只会调用一次
参数: options 不同组件之间传参数
a页面?id=10  b页面:options.id
建议1:通常在此事件发送**ajax请求**
建议2:获取参数 #工具菜单->编译配置
- 3.`onReady` 页面初次渲染完成触发,一个页面只会调用一次,
代表页面己渲染结束可以进入**交互操作**
- 2.`onShow` 页面显示或者**切换前台**时触发,监听页面显示,例如电话中断。
- `onHide` 页面隐藏/切换后台触发,组件依然保留在内存中只是不显示
- `onUnload` 页面卸载时触发.通过程序跳转其它组件
redirectTo();navigateBack()触发
### 组件事件处理函数
- `onPullDownRefresh`监听用户下拉动作
	1. 默认小程序禁止用户下拉操作
	2. 在全局配置文件"window"
		enablePullDownRefresh:false
- `onReachBottom`页面上拉触底
- `onShareAppMessage`用户点击右上角分享
- `onPageScroll`监听用户滑动操作,在垂直方向上的滚动距离。

## 配置 （就近原则）
### [全局配置](https://developers.weixin.qq.com/miniprogram/dev/framework/config.html)
app.json 全局
- pages:  array 页面路径列表
默认显示数组第一个组件内容
- window 窗口样式(渲染方式)
"navigationBarTextStyle": "black"/"white"
	颜色 "#f00" red 错误 
- tabBar 兼容性差
### 局部配置
## 数据表现
**wxml(WeiXin Markup Language)** **一套以xml****为标准语言**
`<view><view> ` div
`<text></text>` 只有text元素才能全选(复制)
:selectable  false 文本是否可以选中
:decode  false 是否解码 &lt;  &gt;
`<image src="x.jpg" mode="aspectFill " lazy-load></image>`
:mode:二个参数选项 "scaleToFill"  "aspectFit" 缩放
:lazy-load:支持懒加载
`<navigator url="当前小程序跳转链接"></navigator>`
定义在tabbar的不能用navigator跳转。
`navigator`将当前组件隐藏
## 数据显示
1. 小程序动态获取对应组件data值,使用方式双大括号
{{msg}}
	- data 属性保存初始化数据
	- 控制属性加在双括号之内
2. `<view  wx:if="{{condition}}"></view>`
condition:值为true显示view中内容
值为false不显示
3. `<view wx:elif="{{}}"></view>`
4. `<view wx:else></view>`
5. `<block></block>`
括号开始括号结束
`wx:if` 是一个控制属性，需要将它添加到一个标签上。如果要一次性判断多个组件标签，可以使用一个 `<block/>` 标签将多个组件包装起来，并在上边使用 `wx:if` 控制属性
>`<block wx:if="{{true}}"> <view> view1 </view> <view> view2 </view> </block>`
6. `<view wx:for="{{数组对象}}"></view>`
:默认情况循环当前元素item下标 index 可修改
`<view wx:for-index="idx"  wx:for-item="obj"></view>`
`:<view wx:key></view>`小程循环元素之前为提高效率有一个排序操作,提供不重复列,没有属性报警告

**手机上浏览不到小程序中图片**
解决方案
- 修改小程序工具配置不验证域名
工具菜单->项目详情->勾选中
[*]不校验合法域名
- 修改请求图片地址不能 127.0.0.1
data:{
list:[{img_url:"http://127.0.0.1/1.jpg"}]
}
[window+r]->cmd->ipconfig
data:{
list:[{img_url:"http://172.163.100.145/1.jpg"}]
}
-手机开热点,连到热点
ipconfig 无线局域网适配器 ..
-重新编译预览上小程序
## 事件
### 事件绑定:
`<view id="tapTest" data-idx="10" bindtap="函数">Clike Me</view>`
### 事件类型:
- tap  :手指触摸后马上离开
- longtap  :手指触摸后，超过 350ms再离开(长按钮) 旧
- longpress :手指触摸后, 超过 350ms再离开  新 1.5.0
### 绑定函数:
在相应的Page对象定义事件处理函数
```
Page({
	函数名:function(event){}
})
```
### 事件对象信息 ：
- type:"tap" 触发事件名称
- target:{id:" tapTest",dataset:{"idx":19}} 触发事件元素
- currentTarget{} 当前元素
- timeStamp: 页面打开到触发事件所经过毫秒数
### 事件传播方式分类
- 冒泡事件:当一个组件上的事件被触发后，该事件会向父节点传递
bind 冒泡事件 bindtap
- 非冒泡事件:一个组件上的事件被触发后，该事件不向父节点传递
catch 非冒泡事件 catchtap
小程序区别事件处理是否使用冒泡方式看前缀
### 获取不同类型参数跳转方式
小程序参数:不推荐使用参数传递数值方式来将参数传递函数内
解决方案: 自定义属性
`<view id="tapName" data-idx="39" bindtap="tapName"></view>`
```
Page({
	tapName:function(event){
		console.log(event.target.dataset.idx);
	}
})
```
### 小程序跳转与参数传递
小程序不同组件之间跳转
- 方式一:标签
`<navigator url="组件路径">
</navigator>`
组件绝对路径:/组件相对路径:
注意:使用标签方式跳转还可后退
- 方式二:编程
	1. `wx.navigateTo({});`
**保留**当前组件跳转到应用内容其它组件
**但不能跳转 tabbar**
	2. wx.navigateBack({url:组件路径})
关闭当前页组件返回上一个组件*或其它组件*
练习:为exam06组件添加一个按钮点击按钮跳转 exam07
传参数?id=101
		- 新问题:获取参数值不能将数值显示模板
解决问题:
(1)在低版本小程序 this.data.id = id; 正确 2017年的版本中
(2)新版本小程序  使用新方法解决 setData
setData({data属性名:数值})
setData将数据**异步更新视图**wxml同时**改变 this.data值**
	3. wx.redirectTo({url:"组件路径"})
关闭当组件跳转到应用内其它个组件，不允许跳转tabbar
关闭当前组件
1:关闭当前组件
2:卸载组件 在卸载之前触发 onUnload
	4. wx.reLaunch({url:"组件路径"})
关闭**所有**  组件，打开到应用内某个组件
	5. wx.switchTab({url:"组件路径"})
跳转到tabBar组件，并关闭所有非tabbar组件
小结:
(1)不同组件之间跳转保留优先 wx.navigateTo()
(2)如果当前组件定义tabbar  wx.reLaunch()
### 小程序--AJAX请求
小程序中显示数据依赖 AJAX获取服务器上数据,
保存当前data属性在模板显示
wx.request({}) 小程序发送异步请求方法
- 常用属性和方法

	- url 请求服务器程序地址
	- data string/object/array 请求参数
	- **method** 请求方法
	- header 请求header appliation/json
	- success 请求成功回调函数
	- fail 请求失败回调函数
	- complete 无论成功或失败都执行

- 常见错误
(1)工具菜单->项目详细->[*] 不校验合法域名
(2) this.setData is not a function;
在请求处理函数this 指定当前 wx对象 wx没有 setData
将this指定从 wx 修改 Page
解决方案:使用箭头函数
(3)参数传递失败 id;age
解决方案:打开网络控制面板 network
### 小程序特性--交互
- `wx.showToast({});` 显示消息提示框
title:".." 提示的内容
icon:"" 图标:默认值 "success"
duration 延迟时间
注意:title字数为了兼容性少于7个字
注意:icon:"success" "loading" "none"
- `wx.showModal({});` 显示模态对话框
title:"" 标题
content:"" 内容
success: (res)=>{
}
练习:
以下view文字切换效果 "收藏" "取消收藏"
<view>收藏</view>
点击view 提示模态框"是否收藏文章"
是:<view>取消收藏</view>
否:<view>收藏</view> ----- res.confirm
- `wx.showActionSheet({})` 显示操作菜单
```
itemList:["","",""]
itemColor:"#fff"
success:(res)=>{
	res.tapIndex 用户选中下标
}
```
### 小程序特性--存储
- **局部**(当前组件)数据存储
`data:{}`
- **全局**(小程序生命周期)数据存储跨组件
	- 在app.js 定义全局共享数据
		```
		App({
		globalData:{LoginName:"",list:[]}
		})
		```
	- 其它组件操作全局数据
		1. 加载全局组件,小程序提供方法 getApp();
			const app = getApp();
		2. 读取数据
			var uname = app.globalData.LoginName;
		3. 操作数据
			app.globalData.LoginName = "tom"
### 小程序特性--音频
小程序后台播放器播放音乐，对于微信客户端来说，只能同时
有一个后台音乐在播放，当其它小程序占用音乐播放器，原有
小程序音乐停止播放
- **方法与事件**
	1. wx.playBackgroundAudio({}) 播放背景音乐
		- datalist 音乐链接
		- 目前支持音频格式 mp3;wav;aac;m4a
		- title 音乐标题
		- convertImgUrl 封面
	2. wx.pauseBackgroundAudio({}) 暂停背景音乐
	3. wx.stopBackgroundAudio({}) 停止背景音乐
	4. wx.onBackgroundAudioPlay 监听音乐播放事件
	5. wx.onBackgroundAudioPause 监听音乐暂停播放事件
	6. wx.onBackgroundAudioStop 监听音乐停止播放事件
- 开发顺序
	1. 将音频文件保存服务器 node.js/public/bg.mp3
	2. 启动服务器
	3. 打开浏览器访问bg.mp3
	4. 组件
*常见错误:音乐播放时闪退
原因:音乐文件路径不正确或者服务器出错*
### 小程序--模板操作
- 创建目录
item_template.wxml
item_template.wxss
- 添加代码
`<template name="item_name">
<view class="item">{{user.name}}<view>
</template>`
.item{color:red}
- 其它组件如何调用[引入模板;引入模板样式文件]
post_item.wxml 文件引入模板
`<import src="item/item_template" />`
post_item.wxss文件引入模板样式文件
`@import "post_item/post_item_template.wxss"`
**注意**:当前版本中不能引模板js文件
- 调用模板
`<template  is="模板名称" data="{{user}}"  />`
**打散参数`...`**
常见错误
(1) Path "..." not found from "./pages/post/post.wxml"
原因:模板路径
(2) Template "post-item1" not found.
原因:名称不同正确
练习:将轮播图功能创建模板保存在post调用
### 小程序--tabbar
小程序主页底层导航条，该导航条是通过配置文件创建app.json
```
	pages:[] 组件访问路径
	windows:{} 组件配置
	tabBar:{
		"position":"bottom",  tabbar位置"top","bottom"
		"list":[
			{
				"pagePath":"pages/home/home",  #访问组件路径
				"text":"首页",  #当前文本
				"iconPath":"assets/tabs/home.png", #图片路径
				"selectedIconPath":"assets/tabs/home-action.png"#选中图片
			}
		]
	}
```
注意
- 图片本地保存
- 最少二个对象

常见错误
- tabBar.list[1].iconPath 文件不存在
tabBar.list[1].selectedIconPath 文件不存在
-点击某个组件 tabbar 消失
-当前组需要显示tabbar必须将组配置
tabbar:[pagePath]
```
/* post请求nodejs端 */
app.post("/postProduct", (req, res) => {
	req.on("data", (buff) => {
		var obj = qs.parse(buff.toString());
		var pno = obj.pno;
		var proce = obj.price;
		res.send({code: 1, msg: "ok"}); 
	})
})
/* page.js */
wx.request({
	method: "POST",
	header: { "Content-Type": "application/x-www-form-urlencoded" }
	...
})
```
```
/* 分页请求page.js中 */
wx.request({
	url: ...
	data: { 
		pno: ++this.data.pageIndex,
		pageSize: this.data.pageSize
	},
	success: (result) => {
		var pageCount = result.data.pageCount;
		var pno = result.data.pageIndex;
		/* 获取返回数据 */
		var flag = pno < pageCount;
		this.setData({
			list: data,
			hasMore: flag
		})
	}
})
```
- 功能一: 如果商家名称过长载取...
`css app.wxss`
- 功能二:上拉显示下一页
```
onReachBottom:{
	this.loadMore();
}
```
- 功能三:只能显示一页改成追加
`var list = this.data.list.concat(result.data.data);
this.setData({list:list});`
- 功能四:如果显示最后一页不能发送请求..
`if(this.data.hasMore==false)return;`
- 功能五:如果没有下一页数据
`<view>己经没有更多的数据了</view>`
- 功能六:如果有下一页数据显示加载动画效果
```
wx.showLoading({
	title:"正在加载数据"
});
setTimeout(function(){
wx.hideLoading();
},1000)
```
### 小程序--多媒体视频
- 通过video组件显示视频
`<video src="视频路径"></video>`
默认视频:300px 宽 225px 高
常见属性
autoplay 自动播放
loop 循环
muted 静音
poster 广告图片
controls 控件
- 通过video组件显示视频(选择视频 相册 照相机)
`<video src="{{src}}"></video>`
```
wx.chooseVideo({  #选择视频播放
	sourceType:["album","camera"],  #相册相机
	maxDuration:60,  #视频长度上限
	camera:["front","back"],  #相册可以用前摄像头后
	success:(result)=>{
		result.tempFilePath;  #视频路径
	}
})
```
### phonegap--混编
- 移动端技术[boostrap;vue;小程序..]
以上移动技术不能调用移动端设备底层硬件加速传感器,
录音;录视频
-实现对底层硬件调用
	1. 方式一:(苹果硬件调用 Object-C)
			:(安卓硬件调用 Java)
	2. 方式二:类似通用平台软件 phonegap
js  -> phonegap -> 硬件
3.4:phonegap--混编
phonegap 是一种使用前端技术(js)创建移动平台，该平台
封装很多JS API，可以使用前端js调用底层设备
(file:///C:/Users/web/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)
3.5:phonegap--创建环境
(1)phonegap 服务器
(file:///C:/Users/web/AppData/Local/Temp/msohtmlclip1/01/clip_image003.png)
1.1 上传程序模板
1.2 点击phonegap 启动服务器
+查找程序模板位置
Open existiong PhoneGap project
1.3 启动服务器
http://172.163.100.145:3000/
注意:如果状态条绿色启动成功
(2)手机模拟器
2.1: 夜神模拟器
2.2: 上传android app
2.3: 点击app连接phonegap
3.6:phonegap--代码
(1)device 硬件设备
device.platform 当前平台
device.uuid 设备编号
device.version 设备版本
(2)相机
navigator.camera.getPicture(fn,fn,{quality:50});
fn: 拍照成功 url 相片地址
fn: 拍照失败
quality:50 延迟时间
(3)提示蜂鸣震动
navigator.notification.alert(); 提示框
navigator.notification.confirm("内容",function(e){}); 确认框
navigator.notification.beep(次数) 蜂鸣器
navigator.notification.vibrate(时长毫秒) 震动
(4)录音
navigator.device.capture.captureAudio(fn,fn,{limit:2});
fn 成功录音结束 list
fn 录音失败
{limit:2} 一次录二段音频
(5)加速传感器
navigator.accelerometer.getCurrentAcceleration(
fn,fn
);
fn: 获取成功 参数 x;y;z
fn: 获取失败
3.6:微信公众平订阅号
(1)概念订阅号
-微信小游戏: 高级游戏引擎
[Cocos Creator:Egret;Layabox]
-微信小程序
[2018初始年]
-订阅号:推荐三年
个人媒体平台:每天向粉丝发送一条消息
消息:[文章;音频;视频]
"菜刀dui"," 菜刀dui 2"
-订阅号分类
-八卦天天有
-胡说(历史;内幕...)
-小众(白骨精)
-热门:"_咪蒙_" 情感
-自己创建订阅号
注册:邮箱 身份证号
(2)订阅号测试帐户开发->聊天工具(不是聊天机器人)
开发者工具->公众平台测试帐户
(1)创建服务器并且合法域名[内网穿透工具]
ngrok.exe  http  3000
https://743f7eb4.ngrok.io
(2)下载第三方微信聊天模块
(3)使用聊天模块调用模块方法完成聊天操作
let config = {
appid:"wx31c2f70c58017a68 "
token:"weixin"
encodingAESKey:""
};
app.post("/",wechat(config,(req,res)=>{
req.weixin.Content 服务器发送文字
res.reply(返回文字);
}));
(4)在测试帐户中
**接口配置信息**
url:[合法域名]  https://743f7eb4.ngrok.io
token:[weixin] 在开发配置项 token一致
**JS****接口安全域名修改**
url:[合法域名]  743f7eb4.ngrok.io
(5)邀请其它用户测试
<![if !vml]>![](file:///C:/Users/web/AppData/Local/Temp/msohtmlclip1/01/clip_image005.jpg)<![endif]>
下载
内网穿透工具: https://ngrok.com/
第三方模块: npm i wechat
常见错误:
(1):在第4步之前启动 node.js 服务器
测试连接发送给node.js get 请求
app.get("/"); 测试连接
app.post("/"); 聊天
(2)服务器故障
-node.js 停止或者代码
-ngrok.exe 重新申请域名
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg3MTI4Nzk3NSwtNDkzMjMzMjk0LC0xMj
Y3MTU0NzgyXX0=
-->