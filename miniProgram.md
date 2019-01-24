---


---

<h2 id="概述">概述</h2>
<ul>
<li>小程序wxml 是一种xml文件用于描述网页结构<br>
xml-格式要求非常严格
<ul>
<li>一个xml文件必须有且只有一个根元素</li>
<li>所有标签有开始必须有结束</li>
<li>属性值必须双引号</li>
</ul>
</li>
<li>组件</li>
<li>rpx和设计稿一致，font-size用px</li>
<li>js程序
<ol>
<li>ECMAScript<br>
基本数据类型：number;string;boolean;null;undefined;<br>
引入				:	Object;Number;Date;RegExp;</li>
<li>小程序没有BOM/DOM概念（document,window,alert()）</li>
<li>小程序顶级对象<code>wx</code></li>
</ol>
</li>
</ul>
<h2 id="生命周期">生命周期</h2>
<p>生命周期:一个组件从创建到销毁过程</p>
<h3 id="全局生命周期app.js">全局生命周期:app.js</h3>
<ul>
<li>onLaunch 当小程序运行只执行一次</li>
</ul>
<h3 id="局部生命周期组件生命周期">局部生命周期(组件生命周期)</h3>
<ul>
<li>1.<code>onLoad</code> 组件加载时触发一个组件只会调用一次<br>
参数: options 不同组件之间传参数<br>
a页面?id=10  b页面:options.id<br>
建议1:通常在此事件发送<strong>ajax请求</strong><br>
建议2:获取参数 #工具菜单-&gt;编译配置</li>
<li>3.<code>onReady</code> 页面初次渲染完成触发,一个页面只会调用一次,<br>
代表页面己渲染结束可以进入<strong>交互操作</strong></li>
<li>2.<code>onShow</code> 页面显示或者<strong>切换前台</strong>时触发,监听页面显示,例如电话中断。</li>
<li><code>onHide</code> 页面隐藏/切换后台触发,组件依然保留在内存中只是不显示</li>
<li><code>onUnload</code> 页面卸载时触发.通过程序跳转其它组件<br>
redirectTo();navigateBack()触发</li>
</ul>
<h3 id="组件事件处理函数">组件事件处理函数</h3>
<ul>
<li><code>onPullDownRefresh</code>监听用户下拉动作
<ol>
<li>默认小程序禁止用户下拉操作</li>
<li>在全局配置文件"window"<br>
enablePullDownRefresh:false</li>
</ol>
</li>
<li><code>onReachBottom</code>页面上拉触底</li>
<li><code>onShareAppMessage</code>用户点击右上角分享</li>
<li><code>onPageScroll</code>监听用户滑动操作,在垂直方向上的滚动距离。</li>
</ul>
<h2 id="配置-（就近原则）">配置 （就近原则）</h2>
<h3 id="全局配置"><a href="https://developers.weixin.qq.com/miniprogram/dev/framework/config.html">全局配置</a></h3>
<p>app.json 全局</p>
<ul>
<li>pages:  array 页面路径列表<br>
默认显示数组第一个组件内容</li>
<li>window 窗口样式(渲染方式)<br>
“navigationBarTextStyle”: “black”/“white”<br>
颜色 “#f00” red 错误</li>
<li>tabBar 兼容性差</li>
</ul>
<h3 id="局部配置">局部配置</h3>
<h2 id="数据表现">数据表现</h2>
<p><strong>wxml(WeiXin Markup Language)</strong> <strong>一套以xml****为标准语言</strong><br>
<code>&lt;view&gt;&lt;view&gt;</code> div<br>
<code>&lt;text&gt;&lt;/text&gt;</code> 只有text元素才能全选(复制)<br>
:selectable  false 文本是否可以选中<br>
:decode  false 是否解码 &lt;  &gt;<br>
<code>&lt;image src="x.jpg" mode="aspectFill " lazy-load&gt;&lt;/image&gt;</code><br>
:mode:二个参数选项 “scaleToFill”  “aspectFit” 缩放<br>
:lazy-load:支持懒加载<br>
<code>&lt;navigator url="当前小程序跳转链接"&gt;&lt;/navigator&gt;</code><br>
定义在tabbar的不能用navigator跳转。<br>
<code>navigator</code>将当前组件隐藏</p>
<h2 id="数据显示">数据显示</h2>
<ol>
<li>小程序动态获取对应组件data值,使用方式双大括号<br>
{{msg}}
<ul>
<li>data 属性保存初始化数据</li>
<li>控制属性加在双括号之内</li>
</ul>
</li>
<li><code>&lt;view wx:if="{{condition}}"&gt;&lt;/view&gt;</code><br>
condition:值为true显示view中内容<br>
值为false不显示</li>
<li><code>&lt;view wx:elif="{{}}"&gt;&lt;/view&gt;</code></li>
<li><code>&lt;view wx:else&gt;&lt;/view&gt;</code></li>
<li><code>&lt;block&gt;&lt;/block&gt;</code><br>
括号开始括号结束<br>
<code>wx:if</code> 是一个控制属性，需要将它添加到一个标签上。如果要一次性判断多个组件标签，可以使用一个 <code>&lt;block/&gt;</code> 标签将多个组件包装起来，并在上边使用 <code>wx:if</code> 控制属性</li>
</ol>
<blockquote>
<p><code>&lt;block wx:if="{{true}}"&gt; &lt;view&gt; view1 &lt;/view&gt; &lt;view&gt; view2 &lt;/view&gt; &lt;/block&gt;</code></p>
</blockquote>
<ol start="6">
<li><code>&lt;view wx:for="{{数组对象}}"&gt;&lt;/view&gt;</code><br>
:默认情况循环当前元素item下标 index 可修改<br>
<code>&lt;view wx:for-index="idx" wx:for-item="obj"&gt;&lt;/view&gt;</code><br>
<code>:&lt;view wx:key&gt;&lt;/view&gt;</code>小程循环元素之前为提高效率有一个排序操作,提供不重复列,没有属性报警告</li>
</ol>
<p><strong>手机上浏览不到小程序中图片</strong><br>
解决方案</p>
<ul>
<li>修改小程序工具配置不验证域名<br>
工具菜单-&gt;项目详情-&gt;勾选中<br>
[*]不校验合法域名</li>
<li>修改请求图片地址不能 127.0.0.1<br>
data:{<br>
list:[{img_url:“<a href="http://127.0.0.1/1.jpg">http://127.0.0.1/1.jpg</a>”}]<br>
}<br>
[window+r]-&gt;cmd-&gt;ipconfig<br>
data:{<br>
list:[{img_url:“<a href="http://172.163.100.145/1.jpg">http://172.163.100.145/1.jpg</a>”}]<br>
}<br>
-手机开热点,连到热点<br>
ipconfig 无线局域网适配器 …<br>
-重新编译预览上小程序</li>
</ul>
<h2 id="事件">事件</h2>
<h3 id="事件绑定">事件绑定:</h3>
<p><code>&lt;view id="tapTest" data-idx="10" bindtap="函数"&gt;Clike Me&lt;/view&gt;</code></p>
<h3 id="事件类型">事件类型:</h3>
<ul>
<li>tap  :手指触摸后马上离开</li>
<li>longtap  :手指触摸后，超过 350ms再离开(长按钮) 旧</li>
<li>longpress :手指触摸后, 超过 350ms再离开  新 1.5.0</li>
</ul>
<h3 id="绑定函数">绑定函数:</h3>
<p>在相应的Page对象定义事件处理函数</p>
<pre><code>Page({
	函数名:function(event){}
})
</code></pre>
<h3 id="事件对象信息-：">事件对象信息 ：</h3>
<ul>
<li>type:“tap” 触发事件名称</li>
<li>target:{id:" tapTest",dataset:{“idx”:19}} 触发事件元素</li>
<li>currentTarget{} 当前元素</li>
<li>timeStamp: 页面打开到触发事件所经过毫秒数</li>
</ul>
<h3 id="事件传播方式分类">事件传播方式分类</h3>
<ul>
<li>冒泡事件:当一个组件上的事件被触发后，该事件会向父节点传递<br>
bind 冒泡事件 bindtap</li>
<li>非冒泡事件:一个组件上的事件被触发后，该事件不向父节点传递<br>
catch 非冒泡事件 catchtap<br>
小程序区别事件处理是否使用冒泡方式看前缀</li>
</ul>
<h3 id="获取不同类型参数跳转方式">获取不同类型参数跳转方式</h3>
<p>小程序参数:不推荐使用参数传递数值方式来将参数传递函数内<br>
解决方案: 自定义属性<br>
<code>&lt;view id="tapName" data-idx="39" bindtap="tapName"&gt;&lt;/view&gt;</code></p>
<pre><code>Page({
	tapName:function(event){
		console.log(event.target.dataset.idx);
	}
})
</code></pre>
<h3 id="小程序跳转与参数传递">小程序跳转与参数传递</h3>
<p>小程序不同组件之间跳转</p>
<ul>
<li>方式一:标签<br>
<code>&lt;navigator url="组件路径"&gt; &lt;/navigator&gt;</code><br>
组件绝对路径:/组件相对路径:<br>
注意:使用标签方式跳转还可后退</li>
<li>方式二:编程
<ol>
<li><code>wx.navigateTo({});</code><br>
<strong>保留</strong>当前组件跳转到应用内容其它组件<br>
<strong>但不能跳转 tabbar</strong></li>
<li>wx.navigateBack({url:组件路径})<br>
关闭当前页组件返回上一个组件<em>或其它组件</em><br>
练习:为exam06组件添加一个按钮点击按钮跳转 exam07<br>
传参数?id=101
<ul>
<li>新问题:获取参数值不能将数值显示模板<br>
解决问题:<br>
(1)在低版本小程序 <a href="http://this.data.id">this.data.id</a> = id; 正确 2017年的版本中<br>
(2)新版本小程序  使用新方法解决 setData<br>
setData({data属性名:数值})<br>
setData将数据<strong>异步更新视图</strong>wxml同时<strong>改变 this.data值</strong></li>
</ul>
</li>
<li>wx.redirectTo({url:“组件路径”})<br>
关闭当组件跳转到应用内其它个组件，不允许跳转tabbar<br>
关闭当前组件<br>
1:关闭当前组件<br>
2:卸载组件 在卸载之前触发 onUnload</li>
<li>wx.reLaunch({url:“组件路径”})<br>
关闭<strong>所有</strong>  组件，打开到应用内某个组件</li>
<li>wx.switchTab({url:“组件路径”})<br>
跳转到tabBar组件，并关闭所有非tabbar组件<br>
小结:<br>
(1)不同组件之间跳转保留优先 wx.navigateTo()<br>
(2)如果当前组件定义tabbar  wx.reLaunch()</li>
</ol>
</li>
</ul>
<h3 id="小程序--ajax请求">小程序–AJAX请求</h3>
<p>小程序中显示数据依赖 AJAX获取服务器上数据,<br>
保存当前data属性在模板显示<br>
wx.request({}) 小程序发送异步请求方法</p>
<ul>
<li>
<p>常用属性和方法</p>
<ul>
<li>url 请求服务器程序地址</li>
<li>data string/object/array 请求参数</li>
<li><strong>method</strong> 请求方法</li>
<li>header 请求header appliation/json</li>
<li>success 请求成功回调函数</li>
<li>fail 请求失败回调函数</li>
<li>complete 无论成功或失败都执行</li>
</ul>
</li>
<li>
<p>常见错误<br>
(1)工具菜单-&gt;项目详细-&gt;[*] 不校验合法域名<br>
(2) this.setData is not a function;<br>
在请求处理函数this 指定当前 wx对象 wx没有 setData<br>
将this指定从 wx 修改 Page<br>
解决方案:使用箭头函数<br>
(3)参数传递失败 id;age<br>
解决方案:打开网络控制面板 network</p>
</li>
</ul>
<h3 id="小程序特性--交互">小程序特性–交互</h3>
<ul>
<li><code>wx.showToast({});</code> 显示消息提示框<br>
title:"…" 提示的内容<br>
icon:"" 图标:默认值 “success”<br>
duration 延迟时间<br>
注意:title字数为了兼容性少于7个字<br>
注意:icon:“success” “loading” “none”</li>
<li><code>wx.showModal({});</code> 显示模态对话框<br>
title:"" 标题<br>
content:"" 内容<br>
success: (res)=&gt;{<br>
}<br>
练习:<br>
以下view文字切换效果 “收藏” “取消收藏”<br>
收藏<br>
点击view 提示模态框"是否收藏文章"<br>
是:取消收藏<br>
否:收藏 ----- res.confirm</li>
<li><code>wx.showActionSheet({})</code> 显示操作菜单</li>
</ul>
<pre><code>itemList:["","",""]
itemColor:"#fff"
success:(res)=&gt;{
	res.tapIndex 用户选中下标
}
</code></pre>
<h3 id="小程序特性--存储">小程序特性–存储</h3>
<ul>
<li><strong>局部</strong>(当前组件)数据存储<br>
<code>data:{}</code></li>
<li><strong>全局</strong>(小程序生命周期)数据存储跨组件
<ul>
<li>在app.js 定义全局共享数据<pre><code>App({
globalData:{LoginName:"",list:[]}
})
</code></pre>
</li>
<li>其它组件操作全局数据
<ol>
<li>加载全局组件,小程序提供方法 getApp();<br>
const app = getApp();</li>
<li>读取数据<br>
var uname = app.globalData.LoginName;</li>
<li>操作数据<br>
app.globalData.LoginName = “tom”</li>
</ol>
</li>
</ul>
</li>
</ul>
<h3 id="小程序特性--音频">小程序特性–音频</h3>
<p>小程序后台播放器播放音乐，对于微信客户端来说，只能同时<br>
有一个后台音乐在播放，当其它小程序占用音乐播放器，原有<br>
小程序音乐停止播放</p>
<ul>
<li><strong>方法与事件</strong>
<ol>
<li>wx.playBackgroundAudio({}) 播放背景音乐
<ul>
<li>datalist 音乐链接</li>
<li>目前支持音频格式 mp3;wav;aac;m4a</li>
<li>title 音乐标题</li>
<li>convertImgUrl 封面</li>
</ul>
</li>
<li>wx.pauseBackgroundAudio({}) 暂停背景音乐</li>
<li>wx.stopBackgroundAudio({}) 停止背景音乐</li>
<li>wx.onBackgroundAudioPlay 监听音乐播放事件</li>
<li>wx.onBackgroundAudioPause 监听音乐暂停播放事件</li>
<li>wx.onBackgroundAudioStop 监听音乐停止播放事件</li>
</ol>
</li>
<li>开发顺序
<ol>
<li>将音频文件保存服务器 node.js/public/bg.mp3</li>
<li>启动服务器</li>
<li>打开浏览器访问bg.mp3</li>
<li>组件<br>
<em>常见错误:音乐播放时闪退<br>
原因:音乐文件路径不正确或者服务器出错</em></li>
</ol>
</li>
</ul>
<h3 id="小程序--模板操作">小程序–模板操作</h3>
<ul>
<li>创建目录<br>
item_template.wxml<br>
item_template.wxss</li>
<li>添加代码<br>
<code>&lt;template name="item_name"&gt; &lt;view class="item"&gt;{{user.name}}&lt;view&gt; &lt;/template&gt;</code><br>
.item{color:red}</li>
<li>其它组件如何调用[引入模板;引入模板样式文件]<br>
post_item.wxml 文件引入模板<br>
<code>&lt;import src="item/item_template" /&gt;</code><br>
post_item.wxss文件引入模板样式文件<br>
<code>@import "post_item/post_item_template.wxss"</code><br>
<strong>注意</strong>:当前版本中不能引模板js文件</li>
<li>调用模板<br>
<code>&lt;template is="模板名称" data="{{user}}" /&gt;</code><br>
<strong>打散参数<code>...</code></strong><br>
常见错误<br>
(1) Path “…” not found from “./pages/post/post.wxml”<br>
原因:模板路径<br>
(2) Template “post-item1” not found.<br>
原因:名称不同正确<br>
练习:将轮播图功能创建模板保存在post调用</li>
</ul>
<h3 id="小程序--tabbar">小程序–tabbar</h3>
<p>小程序主页底层导航条，该导航条是通过配置文件创建app.json</p>
<pre><code>	pages:[] 组件访问路径
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
</code></pre>
<p>注意</p>
<ul>
<li>图片本地保存</li>
<li>最少二个对象</li>
</ul>
<p>常见错误</p>
<ul>
<li>tabBar.list[1].iconPath 文件不存在<br>
tabBar.list[1].selectedIconPath 文件不存在<br>
-点击某个组件 tabbar 消失<br>
-当前组需要显示tabbar必须将组配置<br>
tabbar:[pagePath]</li>
</ul>
<pre><code>/* post请求nodejs端 */
app.post("/postProduct", (req, res) =&gt; {
	req.on("data", (buff) =&gt;## 概述
### 微信开发
- 微信开发的**定义**：
	微信开发及微信公众平台开发，利用微信提供的接口，将企业信息，服务，活动等内容通过微信网页的方式展现给微信用户。
- 微信开发的**目标**：
	减少宣传成本，建立企业与消费者，客户的一对一互动和沟通，将消费者接入企业CRM系统，进行促销，推广，宣传，售后等；形成线上线下微信互动营销方式。
- 微信开发主要功能或者说针对方向：
	- 在线营销：向终端客户推荐新品，促销策略等；
	- 售后服务，通过微信平台，自动与客户进行交互，展示企业商品，售后支持；
	- 电子商务，将企业网站或购物平台与微信对接，推荐到朋友圈获取免费宣传；
	- 会员管理，企业会员可通过微信平台进行线下活动预约，积分管理等操作。
- 微信开发九大接口：
	1. 语音识别接口
	2. 客服接口
	3. OAuth2.0网页授权接口
	4. 生成带参数的二维码接口
	5. 获取用户地理位置接口
	6. 获取用户基本信息接口
	7. 获取关注者列表接口
	8. 用户分组接口
	9. 上传下载多媒体文件接口
- 微信开发种类：
	- 移动应用开发
		原生Android、iOS中调用微信开发接口，实现微信分享，微信收藏，微信支付
	- 网站应用开发
		让网站支持微信账号快速登录，降低注册门槛；同时授权获取用户基本信息
	- 公众账号开发
		分为：
		- 服务号，商品销售，用户跟踪服务，服务交互，给企业组织提供更强大的业务服务与用户管理能力，帮助企业快速实现全新的公众服务平台。认证服务号可以使用九大高级接口，可申请开通微信支付，其他不能。每月可群发4条消息。
		- 订阅号，单向的向用户推送消息，达到宣传效果，可每天群发1条消息，显示在订阅号文件夹中
		- 企业号，管理内部企业员工团队，主要用于公司内部通讯使用，需要先有成员的通讯信息验证才可以关注成功企业号。同订阅号“群发，显示”。		
	- 公众号第三方平台开发 
- 微信JS-SDK
	是微信公众平台面向网页开发者提供的基于微信内的网页软件开发工具包，
	通过微信JS-SDK，网页开发者可以借助微信高效的使用拍照，选图，语音，位置等手机系统的能力，同时可以直接使用微信分享，扫一扫，卡券，支付等微信特有的能力，为微信用户提供更优质的网页体验。包括地理位置接口，图像接口等。
	JS-SDK使用步骤
	1. 绑定域名
	2. 引入JS文件
	3. 通过config接口注入权限验证配置
	4. 通过ready接口处理成功验证
	5. 通过error接口处理验证失败
### 小程序 
- 简介：是一种不需要下载安装即可使用的应用APP，是一种寄宿于微信中的代码片段，，不等于应用级APP，不等于网站，不等于webAPP.
- 特点：
	- 小：程序小于2M，占用内存小，不需要安装支持底层调用的程序（封装接口）
	- 方便: 使用方便,卸载方便
	- 门槛低：前端兼职开发
	- 成本低：平台大，流量多，推广成本低
	- 兼容性：跨平台
- 小程序app文件构成
	- app.json全局配置信息
	- app.js全局事件处理，全局变量
	- app.wxss公用样式表
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
## wxml语法
### wxml基础语法
- wxml语法基础
	- 数据绑定
	- 数据获取
	- 数据修改
	- 简单事件bindtap
- 交互区别
	- 修改innerHTML：
		小程序无DOM，使用变量修改
	- 修改style
		style="display:{{val}}" 
	- 修改class
		class="{{val}}"
	- 定时修改内容
### wxml高级语法
- 条件渲染
	- tab选项卡
	- 事件传参：dataset
	- 条件渲染
- 列表渲染
	- 列表渲染：wx:for
	- 模板渲染	
- 复杂事件
	- 复杂事件 binglongtao,bindtouchstart,..catch冒泡与否，可使用复杂事件实现小程序版本的图片放大器。
	- 获取输入内容：bindinput，e.detail.value
- 引用
	- wxml分片
		- template
		- `<include src="header.wxml">`
	- js分片
		- com.js `moudule.exports.fnname = value`
		- page: `var value = require('com.js'); say:function() {value.fnname};`
## 小程序组件
### 标记列表
- 视图容器：view,swipe,icon(type,size,color),text(selectable),progress(percent,show-info,color,activeColor,backgroundColor)
- 基础内容
### [表单组件](https://developers.weixin.qq.com/miniprogram/dev/component/)
- 表单组件概述
	- form：
		bindsubmit/bindreset/report-submit
	- input, 
		placeholder,disbaled,maxlength,focus,confirm-type,form-type(submit/reset)...
	- label, 
		for
	- checkbox-group, 
		bindchange,checked,disbaled,color,value
	- checkbox, 
		bindchange,checked,disbaled,color,value
	- radio-group, 
		bindchange,checked,disbaled,color,value
	- radio,
		bindchange,checked,disbaled,color,value
	- button, 
		size(default,mini),type(primary,default,warn),plain(背景透明)，form-type...
	- textarea, 
		value,placeholder,max-length,auto-focus,bind-blur,bindlinechange,bindinput,bindconfirm,cursor-spacing
	- slider,
		step,min, max, selected-color,show-value,bindchange...
	- switch(开关),
		checked, type(switch,checkbox), bindchange, color
	- picker(日期)，
		range, range-key, value, bindchange, disabled
	- pick(复选框)
		start, end, bindchange, disabled, value
	- pick-view-column
		value, indicator-style, bindchange
- form
- 简单组件
- 复杂组件
### 其他组件
- 导航
	- navigator
		url, redirect, open-type(navigate,redirect,switchtab), hover-class, hover-start-time, hover-stay-time
- 媒体组件
	- audio
		id, src, loop, controls, poster, name, author, binderror, bindplay, bindpause, bindtimeupdate(播放进度改变), bindended
	- video
		src, controls, danmu-list, danmu-btn, enable-danmu, bindplay, bindpause, bindtimeupdate, objectFit(cover,contain)
	- image
		src, mode, binderror, bindload(图片载入完毕，event.detail={height:图片高度px, width...})
- 地图
	- map
		include-points, show-location, ...
- 画布
	- canvas
- 会话服务	
	- contact-button客服会话
## [小程序API](https://developers.weixin.qq.com/miniprogram/dev/api/)
### 接口概述
- 接口的支持
### 网络和媒体
- 网络
- 媒体
### 文件和缓存
- 文件
- 数据缓存
### 其他常用接口
- 位置
- 设备
- 界面
- 开放接口
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
</code></pre>
<pre><code>```
```
/* 分页请求page.js中 */
wx.request({
	url: ...
	data: { 
		pno: ++this.data.pageIndex,
		pageSize: this.data.pageSize
	},
	success: (result) =&gt;> {
		var pageCount = result.data.pageCount;
		var pno = result.data.pageIndex;
		/* 获取返回数据 */
		var flag = pno &lt;< pageCount;
		this.setData({
			list: data,
			hasMore: flag
		})
	}
})
</code></pre>
<ul>
<li>功能一: 如果商家名称过长载取…<br>
<code>css app.wxss</code></li>
<li>功能二:上拉显示下一页</li>
</ul>
<pre><code>onReachBottom:{
	this.loadMore();
}
</code></pre>
<ul>
<li>功能三:只能显示一页改成追加<br>
<code>var list = this.data.list.concat(result.data.data); this.setData({list:list});</code></li>
<li>功能四:如果显示最后一页不能发送请求…<br>
<code>if(this.data.hasMore==false)return;</code></li>
<li>功能五:如果没有下一页数据<br>
<code>&lt;view&gt;己经没有更多的数据了&lt;/view&gt;</code></li>
<li>功能六:如果有下一页数据显示加载动画效果</li>
</ul>
<pre><code>wx.showLoading({
	title:"正在加载数据"
});
setTimeout(function(){
wx.hideLoading();
},1000)
</code></pre>
<h3 id="小程序--多媒体视频">小程序–多媒体视频</h3>
<ul>
<li>通过video组件显示视频<br>
<code>&lt;video src="视频路径"&gt;&lt;/video&gt;</code><br>
默认视频:300px 宽 225px 高<br>
常见属性<br>
autoplay 自动播放<br>
loop 循环<br>
muted 静音<br>
poster 广告图片<br>
controls 控件</li>
<li>通过video组件显示视频(选择视频 相册 照相机)<br>
<code>&lt;video src="{{src}}"&gt;&lt;/video&gt;</code></li>
</ul>
<pre><code>```
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
	success:(result)=&gt;>{
		result.tempFilePath;  #视频路径
	}
})
</code></pre>```
### 小程序-上传图片
1. 小程序-上传文件(服务器)node.js
- 加载第三方模块 multer 下载安装
	- 先加载模块创建对应对象
		var upload = multer({dest:”upload/”})
	- 如果模块加载成功req添加属性file
		app.post(“/uploads”,upload.single(“mypic”),(req,res)=>{
		});
- 保存上传文件信息
	req.file.size 上传文件大小 (单位字节)
	req.file.mimetype 上传文件类型
	req.file.originalname 上传文件原名称 1.jpg
	req.file.path 临时文件路径
2.  小程序-上传文件(小程序中)
	- wx.chooseImage();
	从本地相册选图片或使用相机拍照
	count:1 最多可以选择图片总数:9
	sourceType:[“camera”,”album”]指定来源相册还是相机
	success:res 选择成功
	tempFilePaths Array 本地图片路径列表
	fail
	- wx.uploadFile({})
	将本地资源上传到服务器客户端发起POST
	url: 服务器端程序路径
	filePath: 要上传文件资源本地路径
	name: 上传图片name “mypic”
	header 请求头
	“Content-Type”:”multipart/form-data”
	success 上传图片成功

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjAzNjE2MzhdfQ==
-->