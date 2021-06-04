1. CSS模块
  * style样式
    * css(styleName): 根据样式名得到对应的值
    * css(styleName, value): 设置一个样式
    * css({多个样式对}): 设置多个样式
  * 位置坐标
    * offset(): 读/写当前元素坐标(原点是页面左上角)
    * position(): 读当前元素坐标(原点是父元素左上角)
    * scrollTop()/scrollLeft(): 读/写元素/页面的滚动条坐标
  * 尺寸
    * width()/height(): width/height
    * innerWidth()/innerHeight(): width + padding
    * outerWidth()/outerHeight(): width + padding + border
2. 筛选模块
  * 过滤
    * 在jQuery对象内部的元素中找出部分匹配的元素, 并封装成新的jQuery对象返回
    * first()
    * last()
    * eq(index)
    * filter(selector): 对当前元素提要求
    * not(selector): 对当前元素提要求, 并取反
    * has(selector): 对子孙元素提要求
  * 查找
    * 查找jQuery对象内部的元素的子孙/兄弟/父母元素, 并封装成新的jQuery对象返回
    * children(selector): 子元素
    * find(selector): 后代元素
    * preAll(selector): 前的所有兄弟
    * siblings(selector): 所有兄弟
    * parent(): 父元素
3. 文档处理(CUD)模块
  * 增加
    * append() / appendTo(): 插入后部
    * preppend() / preppendTo(): 插入前部
    * before(): 插到前面
    * after(): 插到后面
  * 删除
    * remove(): 将自己及内部的孩子都删除
    * empty(): 掏空(自己还在)
  * 更新
    * replaceWith()
  
4. 事件模块
  * 绑定事件
    * eventName(function(){})
    * on('eventName', function(){})
    * 常用: click, mouseenter/mouseleave mouseover/mouseout focus/blur
    * hover(function(){}, function(){})
  * 解绑事件
    * off('eventName')
  * 事件委托
    * 理解: 将子元素的事件委托给父辈元素处理
      * 事件监听绑定在父元素上, 但事件发生在子元素上
      *　事件会冒泡到父元素
      * 但最终调用的事件回调函数的是子元素: event.target
    * 好处
      * 新增的元素没有事件监听
      * 减少监听的数量(n==>1)
    * 编码
      * delegate(selector, 'eventName', function(event){}) // 回调函数中的this是子元素
      * undelegate('eventName')
  * 事件坐标
     * event.offsetX: 原点是当前元素左上角
     * event.clientX: 原点是窗口左上角
     * event.pageX: 原点是页面左上角
  * 事件相关
    * 停止事件冒泡: event.stopPropagation()
    * 阻止事件的默认行为: event.preventDefault()