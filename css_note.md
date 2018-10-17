## css概述
1.  css概述
	1. css作用
		样式重用和可维护性
	2. 什么是css(Cascading Style Sheets层叠样式表)
		- 实现了将内容和表现分离
		- 提高代码的可重用性和维护性  
	3. css与html之间的关系
		html:构建网页机构
		css:页面的表现
	4. html属性与css样式的使用规则
		尽量内容与变现分离
2.  使用css样式表
	 使用css样式表的方式
	- 内联样式:	使用`;`隔开不同属性
	- 内部样式表
		在当前页面范围内重用
	- 外部样式表
		`<link rel="stylesheet" type="text/css" href="XXX.css"/>	`
## css语法
1.  css语法规范
	1. css语法规范总结
		- 样式表: 选择器+样式声明(属性+值...)
		- 内联: 样式声明
	2. **css样式表特征**
		- 继承和层叠	: *css层叠管理: 同时也是处理css的继承问题的关键*
			- `inherit`关键字使得元素获取其父元素的计算值()注意隔代是否能继承问题,) 它可以应用于任何CSS属性，包括CSS简写“all”。
			- `initial`是将属性的初始值赋给元素 . initial 适用于所有的css 属性，包括css 简写属性(全局属性)[`all`]
			>-   当元素的一个**继承属性**没有指定值时，则取父元素的同属性的**计算值**，只有文档根元素取该属性的概术中给定的**初始值**
			>-   当元素的一个**非继承属性**没有指定值时，则取属性的**初始值**	
			- `unset`如果为继承属性,相当于`inherit`;如果为非继承属性,相当于`initial`.
			- `revert`以前被称为`default`表示没有使用任何属性值.目前(2018-09)仅safari支持,尴尬...
			- `all`属性:包含三个值initial/inherit/unset
			----
			*ps*: 
				- [CSS  Reference](https://www.w3schools.com/cssref/): 属性->Inherited
				- 浏览器中元素调用样式的过程:
						1. User Defined Stylesheet
						2. User Agent Stylesheet
						3. 元素应用`unset`
			
			---
		
	3. 样式优先级
			(由低到高)
			-  浏览器缺省设置
			- 外部样式/内部样式(就近优先)
			- 内联
	4. !important
	5. css设计代码的结构
		- 一般性样式
			```
			/* @group general styles
			------------------------------------*/
			```
			- 主体样式
			- reset样式
			- 链接
			- 标题
			- 其他元素
		- 辅助样式
			```
			/* @group helper styles
			------------------------------------*/
			```
			- 表单
			- 通知和错误
			- 一致的条目
		- 页面结构
			```
			/* @group page structure
			------------------------------------*/
			```
			- 标题,页脚和导航
			- 布局
			- 其他页面结构元素
		- 页面组件
			```
			/* @group page components
			------------------------------------*/
			```
			各个页面
		- 覆盖
			```
			/* @group overrides
			------------------------------------*/
			```
2.  css选择器
	1. 通用选择器`*`
	2. 元素选择器  
	3. 类选择器
	4. id选择器
	5. 群组选择器: `,`隔开
	6. 后代选择器
	7. 子代选择器: `>`作为子结合符,选择某个后代
	8. 伪类选择器
			- 链接伪类: `:link`,`:visited`
			- 动态伪类: `:hover`,`active`, `focus`
			- 目标伪类
			- 元素状态伪类
			- 结构伪类
			- 否定伪类
	9. **选择器优先级**
## 尺寸与边框
1.  css单位
	1. 尺寸单位
		%/in/cm/mm/pt/px/em/rem
	2. 颜色单位
		rgb(x,x,x)/rgb(x%,x%,x%)/#rrggbb/#rgb/颜色英文单词
2.  尺寸属性
	1. 尺寸(像素/百分比)
		width/max-width/min-width/...
	2. 溢出
		`overflow`: 当内容溢出元素框是如何处理
			- `visible`: 
			- `hidden`
			- `scroll`
			- `auto`
	3. 哪些HTML元素可以设置尺寸属性
			- 块级元素
				p/div/hn/ul/ol/li/dt/dl/dd...
			- 存在width/height属性的html元素
				img/table
3. 边框属性 
	1. 边框
		`border: _border-width_  _border-style_  _border-color_|initial|inherit;`
		border-color:transparent创建有宽度的不可见边框
	2. 边框倒角
		`border-radius`: 顺时针设置
	3. 边框阴影
		`box-shadow`:  none|_h-offset v-offset blur spread color_ |inset|initial|inherit;
		- `h-offset`:必需,水平阴影位置
		- `v-offset`:必需
		- `blur`: 模糊距离
		- `spread`: 阴影的尺寸
		- `color`:
		- inset: 改为内部阴影
	4. 轮廓
		
## 框模型
1.  框模型
		![ilRsy9.png](https://s1.ax1x.com/2018/09/30/ilRsy9.png)
2. 外边距
	1. 什么是外边距
	2. 外边距margin
		auto: 由浏览器计算
	3. 外边距的简写
		marign: value(上下) value(左右)
		margin: value(上) value(左右) value(下)
	4. 外边距合并
		垂直外边距合并,以高度较大者为外边距
3.  内边距
	1. 什么是内边距
		内容和边框之间.不能为负值
	2. 内边距padding
	3. 内边距简写
## 背景
1. 背景概述
	背景属性的作用
2. 背景属性
	1. 背景色background-color
	2. 背景图片
	3. 背景重复repeat
	4. 背景图片尺寸size
	5. 背景图片的固定attachment
	6. 背景定位position
	7. 背景属性background
## 渐变
- 渐变属性
	1. 什么是渐变
	2. 渐变语法
	3. 线性渐变
	4. 径向渐变
	5. 重复渐变
	6. 浏览器兼容性 
## 文本格式化
1. 文本格式化描述
2. 字体属性
	 1. 控制字体
	 2. 字体属性font
3. 文本属性
	- 控制文本格式
## 表格
1. 表格常用样式属性
	1. 表格常用样式属性
	2. 垂直方向对齐
2. 表格特有样式属性
	1. 边框合并`border-collapse`
	2. 边框边距`border-spacing`
	3. 标题位置`caption-side`
	4. 显示规则`table-layout`
## 浮动
1. 定位概述
	1. 定位概述
	2. 普通流定位
2. 浮动定位
	1. 浮动概述
	2. 浮动定位
	3. float属性
	4. clear属性
	5. float与overflow
## 显示
1. 显示方式
	- 显示方式
		"一切皆为框":页面上所有的元素都可以显示为框
	- display属性:改变生成的框类型
		**`display:none`不占据空间**
2. 显示效果
	- visibility属性
		- visible
		- hidden:**占据空间**
		- colllapse;用在表格元素时,可删除一行或一列,且不影响表格布局
	- opacity属性
		与rgba()中alpha的透明度区别:opacity作用在元素,会改变所有与元素相关的颜色透明度.
	- vertical-align属性
		定义行内元素的基线相对于该元素所在的行的基线的垂直 对齐对齐.
		- baseline:父元素基线
		- sub/super:文本上下标
		-  top/bottom:元素顶端与行中最高/最低元素的顶端/顶端对齐
		- text-top/text-bottom:把元素与父元素字体相对齐
		- middle:把元素放在父元素的中部.
		- %:使用"line-height"属性的百分比来排列此元素
		- inherit
3. 光标
	 光标
	cursor属性
## 列表
- 列表样式
1. 列表项标志list-style-type
2. 列表项图像list-sytle-image
3. 列表项位置list-sytle-postion
4. 列表属性list-style
## 定位
1. 定位概述
	1. 什么是定位
	2. 定位属性
		position
			将元素的position属性定义为relative/absolute/fixed,这个元素就叫已定位元素
			已定位元素,才能用偏移属性top/bottom/left/right
2. 定位方式
	1. 相对定位
		元素脱离文档流,但是原来的位置不被其他文档中元素占用
	2. 绝对定位
		- 元素脱离默认文档流,原来位置被其他没有脱离文档流的元素占用.
		- **所有的层叠效果,都要使用`absolute`**
		- 绝对定位的参照物:	
			- 如果该元素的父元素是已定位元素,以父元素的左上角为基点定位
			- 如果该元素的父元素不是已定位元素,向上再找一层,直到找到是定位元素的父级,以那层父元素为基准定位
			- 该元素没有是定位元素的祖先元素,以`body`为基准	
	3. 堆叠顺序
	4. 固定定位
