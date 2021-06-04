###BOM
	ECMAScript 是 JavaScript 的核心，但如果要在 Web 中使用 JavaScript，那么 BOM（浏览器对象模型）
	则无疑才是真正的核心。BOM 提供了很多对象，用于访问浏览器的功能，这些功能与任何网页内容无关。多年来，
	缺少事实上的规范导致 BOM 有很多问题，因为浏览器提供商会按照各自的想法随意去扩展它。W3C 为了把浏览器中
	JavaScript 最基本的部分标准化，已经将 BOM 的主要方面纳入了 HTML5 的规范中。
	
###window对象
	BOM 的核心对象是 window，它表示浏览器的一个实例。在浏览器中，window 对象有双重角色，
	它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。
	这意味着在网页中定义的任何一个对象、变量和函数，都以 window 作为其 Global 对象，因此有权访问 
	isNaN()、isFinite()、parseInt()、parseFloat() 等方法。
	
###全局变量与windows对象属性的差别
	抛开全局变量会成为 window 对象的属性不谈，定义全局变量与在 window 对象上直接定义属性还是有一点差别：
	全局变量不能通过 delete 运算符删除，而直接在 window 对象上的定义的属性可以
	
###window.open()/close方法
	open方法的四个参数：可以接收4个参数：要加载的URL、窗口目标、一个特性字符串、
								   一个表示新页面是否取代浏览器历史记录中当前加载页面的布尔值
					后两个参数有很大的兼容性问题			  
								   
	close() 方法仅适用于通过 window.open() 打开的弹出窗口。对于浏览器的主窗口，如果没有得到用户的允许是不能关闭它的。

###定时器
	// 不建议传递字符串
	setTimeout("console.log('Hello world!') ", 1000);
	
	// 推荐的调用方式
	setTimeout(function() { 
	    console.log("Hello world!"); 
	}, 1000);
	
	第二个参数是一个表示等待多长时间的毫秒数，但经过该时间后指定的代码不一定会执行。
	JavaScript 是一个单线程序的解释器，因此一定时间内只能执行一段代码。为了控制要执行的代码，
	就有一个 JavaScript 任务队列。这些任务会按照将它们添加到队列的顺序执行。
	setTimeout() 的第二个参数告诉 JavaScript 再过多长时间把当前任务添加到队列中(添加的过程是异步的)。
	如果队列是空的，那么添加的代码会立即执行；如果队列不是空的，那么它就要等前面的代码执行完了以后再执行。
###navigator对象
###location对象
	location 对象是很特别的一个对象，因为它既是 window 对象的属性，也是 document 对象的属性；
	换句话说，window.location 和 document.location 引用的是同一个对象。
###history 对象	
