#### v-model 的实现原理

v-model其实是个语法糖，它实际上是做了两步动作：
**1、绑定数据value**
**2、触发输入事件input**

```vue
<template>
  <div id="app">
    {{username}} <br/>
    <input type="text" :value="username" @input="username=$event.target.value">
    //当你触发input事件时，$event 是当前的事件对象。 $event.target.value指向的是当前的input的值
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      username:''
    }
  }

}
</script>
```

在 Vue 中通过索引值来改变数组中的值不是响应的

因为 Vue 没有监听通过这种方式来改变数组，所以 Vue 不会刷新界面

哪些方法是响应式的

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>

<script src="../vue/vue.js" type="text/javascript" charset="utf-8"></script>
  <div id="app">
		<ul>
			<li v-for="item in letters">{{item}}</li>
		</ul>
		<button @click="click">按钮</button>
  </div>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message:'你好啊',
				letters: ['a','b','c','d']
      },
      methods: {
				click(){
					//1. pop()方法：删除数组中最后一个元素
					// this.letters.pop();

					//2. shift()方法：删除数组中第一个元素
					// this.letters.shift();

          //3. push()方法：在数组最后追加 一个 或 多个 元素
          // this.letters.push('aaa');
          // this.letters.push('aaa','bbb','ccc');

					//4. unshift()方法：在数组最前面添加 一个 或 多个 元素
					// this.letters.unshift('aaa');
					// this.letters.unshift('aaa','bbb','ccc');

					//5. splice()方法: 删除元素/插入元素/替换元素
					//删除元素：第一个参数是从哪里开始删除，第二个参数是删除几个元素，如果不写，会删除后面的所有元素
					// this.letters.splice(1,2);
          // this.letters.splice(1);

          //插入元素：第一个参数是从哪里开始插入，第二个参数是0，后面跟着你要插入的元素
          // this.letters.splice(1,0,'rrrr','bbb');

					//替换元素：第一个参数是从哪里开始替换，第二个参数是替换几个，后面跟着你要替换的元素
          // this.letters.splice(2,1,'rrrr');
          // this.letters.splice(2,1,'rrrr','ssss');

					//6. sort()方法：对数组元素进行排序
					// this.letters.sort();

					//7. reverse()方法：对数组元素进行反转
					// this.letters.reverse();
          
          //8.vue 的 set() 方法
					/*
					* 第一个参数：要修改的对象
					* 第二个参数：想要修改的的元素的索引值
					* 第三个参数：修改后的值
					* */
					Vue.set(this.letters,0,'bbbbb')
				}
			}
    });
	</script>

</body>
</html>

```

