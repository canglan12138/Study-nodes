###Welcome to use MarkDown
	正如W3C所定义的，DOM是独立于平台和语言的接口，该接口为程序和脚本提供了对文档的内容、
	结构和样式的动态获取和更新的功能。

	DOM的出现来自对动态页面的需求，先有DOM的实现（Netscape DOM0），再有各个厂商对DOM实现规范的需求，
	再有了W3C Activity Statement对于DOM发展的规范，然后才有了我们所说的“DOM”。

	DOM0：不是W3C规范。
	DOM1：开始是W3C规范。专注于HTML文档和XML文档。
	DOM2：对DOM1增加了样式表对象模型(DOM2)
	DOM3：对DOM2增加了内容模型 (DTD 、Schemas) 和文档验证。

	DOM0指的是Necscape3.0和IE3.0提供对于HTML文档功能，实现了包括元素(HTML Element)、表单(Form)、
	图像(Image)等的接口和方法。DOM0虽然年代久远，某些实现并不符合新的DOM理念，但为了向后兼容，
	很多现代浏览器仍然支持DOM0的某些方法和属性。即便某些方法的实现原理有所不同，但提供了可用性。
	DOM0出现后，各厂商意识到DOM的前景，纷纷向W3C建议DOM的规范化。
		于是出现了W3C DOM Activity Statement（DOM的活动清单）以及DOM1、DOM2、DOM3规范(Specification)
	
	DOM1 1.0版本发布于1998年10月1日，是第一个DOM规范。DOM1包含两部分:
		DOM1 Core：定义了DOM最基本的接口，包括Document，Node，NodeList等等。
		DOM1 THML：HTML文档是DOM的一种实现，该规范定义了基于DOM1 Core的HTML文档实现。
	
	DOM2规范在2000年11月13日发布，主要包含6个模块，相比于DOM1，DOM2更加丰富，更加完善，
		目前主流浏览器对DOM2有着良好的支持。
		DOM2 Core: 相比于DOM1 Core，DOM2丰富了Document，Node等接口的功能，
		DOM2 View：View提供的是DOM的表现形式，同一个文档源(document source)，可能有不同的表现形式，
					DOM2 View引入了Abstract View和Document View接口。
		DOM2 Event：DOM 事件处理系统规范，DOM1中并未对DOM的事件模型进行定义，
					在DOM2中规范事件模型(Event Model)主要有两个目的：
						1)设计一套通用的事件系统，实现事件处理程序的注册和注销，描述事件的流动(Event Flow)，
							事件的上下文信息(Contextual Information )等；
						2)提供一套规范子集兼容老版本浏览器DOM0的事件实现。
		DOM2 Style：程序和脚本动态地获取和更新DOM的样式，提供包括Style Sheet, 
					Cascading Style Sheet, CSSRule, CSSStyleDeclaration, getComputedStyle接口。
					DOM2 Style的实现基于DOM2 Core和DOM2 View。
		DOM2 Traverse and Range：DOM2 Traverse是关于文档节点遍历的规范，
					包括Treewalker，NodeIterator和NodeFilter等；
					DOM2 Range是关于DOM片段(Document Fragment)操作的规范，譬如DocumentFragment。
		DOM2 HTML：在DOM1 HTML的基础上结合DOM2 Core推出了一些新的接口和属性

	DOM3首次发布于2004年4月，主要包括Core、Load and Save、Validation、XPath、View and Formatting、
		Events和Abstract Schemas7个模块。目前主流浏览器对DOM3的支持比较有限