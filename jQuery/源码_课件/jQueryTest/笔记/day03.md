* 动画效果
  * 在一定的时间内, 不断改变元素样式
  * slideDown()/slideUp()/slideToggle()
  * fadeOut()/fadeIn()/fadeToggle()
  * show()/hide()/toggle()
  * animate({结束时的样式}, time, fun)
  * stop()

* 插件机制
  * 扩展jQuery函数对象的方法
    $.extend({
      xxx: fuction () {} // this是$
    })
    $.xxx()
  * 扩展jQuery对象的方法
    $.fn.extend({
      xxx: function(){}  // this是jQuery对象
    })
    $obj.xxx()
    
* jQuery文档的结构图