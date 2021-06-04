### 两种绑定方式
	(DOM0)1.obj.onclick = fn;	
		
	(DOM2)2.
	  ie:obj.attachEvent(事件名称，事件函数);
		1.没有捕获(非标准的ie 标准的ie底下有  ie6到10)
		2.事件名称有on
		3.事件函数执行的顺序：标准ie-》正序   非标准ie-》倒序
		4.this指向window
	      标准:obj.addEventListener(事件名称，事件函数，是否捕获);
		1.有捕获
		2.事件名称没有on
		3.事件执行的顺序是正序
		4.this触发该事件的对象
		
		
		document.attachEvent('onclick', fn2);
		document.attachEvent('onclick', function() {
			fn1.call(document);
		});
		
		是否捕获 : 默认是false    false:冒泡 true：捕获
		
		document.addEventListener('click', fn1, false);
		document.addEventListener('click', fn2, false);
			
	注意
		ie代表了:非标准ie 和 标准ie
		标准代表了:标准ie 和 chrome Firefox等....

### 同步this
	function bind(obj, evname, fn) {
		if (obj.addEventListener) {//除ie低版本外都可以进入
			obj.addEventListener(evname, fn, false);
		} else {
			obj.attachEvent('on' + evname, function() {
				fn.call(obj);
			});
		}
	}

	bind(document, 'click', fn1);
	

### 两种绑定方式的区别
	取消冒泡的手段:event.cancelBubble = true;
		   	    event.stopPropagation();

	第一种:默认冒泡,
	第一种:一个元素上只能绑定一个同类事件,如果继续绑定的话,第二个事件函数会覆盖第一个
	
	
	第二种: 
		  attachEvent
		  			       默认冒泡
		  addEventListener    
					      是否捕获 : 默认是false    
					      第三个参数: false:冒泡
							    true：捕获
	第二种:一个元素上可以绑定多个同类事件,它们都会被执行


### 事件解绑
	DOM0:想解除事件就相当简单了，只需要再注册一次事件，把值设成null
			原理就是最后注册的事件要覆盖之前的，最后一次注册事件设置成null，
				也就解除了事件绑定。
				
	DOM0事件模型还涉及到直接写在html中的事件:
			因此不会传入event对象，同时，this指向的是window，不再是触发事件的dom对象。
			
	DOM2:removeEventListener
		 	解除事件语法：btn.removeEventListener("事件名称", "事件回调", "捕获/冒泡");
		 detachEvent(ie)
		 	
### 事件流
	单击蓝色框后，开始事件捕获阶段：
		从最外层的document对象（浏览器其实是从window对象开始的）向内捕获事件，路过红色框时，查看到红色框有事件，
		但是红色框说：“我是在冒泡阶段执行，现在是捕获阶段，等你回来再说吧。”
		接下来是黄色框：“我在捕获阶段执行，就是现在执行！在控制台输“黄色框”吧~~”
	接下来到达目标阶段：
		“DOM2级事件”规范要求捕获阶段不会涉及事件目标即我们点击的那个最具体的元素，
		但IE9、Chrome等浏览器都会在捕获阶段触发事件对象上的事件。执行目标对象的事件函数，控制台输出“蓝色框”。
	最后是冒泡阶段：
		由目标对象向外传递，到达黄色框，黄色框说：“我在捕获阶段执行过了，你走吧...”
		然后到达红色框，红色框说：“你终于回来了，现在就执行我的事件！”控制台输出“红色框”。
		然后继续向外传播，直到到达document对象后停止。
	其他：更改了元素绑定事件代码的顺序，执行顺序也和上面表现的一致。

### 总结
	onclick形式:冒泡
	attachEvent:冒泡
	addEventListener:第三个参数(false:冒泡;true:捕获)