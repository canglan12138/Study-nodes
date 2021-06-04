# JS把变量存哪了？

在JS中变量是用来存储对象的，但变量也属于程序中的一部分，也要存储到内存之中，那么就产生了一个问题，变量存储在哪里呢？

这一点我们之前曾经提到过，变量被存储到一个名为“变量对象”的对象中。所谓的创建变量其实就是向“变量对象”中添加属性。那么变量对象是什么样子呢？我们能否看到呢？其实通过一些工具我们是可以看到变量对象的。举个例子，有如下js代码，写在了index.html文件中。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-16.png)



通过Chrome浏览器来运行网页，并打开开发者工具，切换到Sources标签，并点击左侧的index.html。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-17-1024x360.png)

​																													*开发者工具*



Chrome的开发者工具中Sources标签表示源码，通过Sources可以直接查看网页的源码，点击index.html的目的是告诉浏览器我要看的是index.html的源码。

Sources窗口的右侧表示网站的文件列表，中间区域用来显示代码的具体内容，右侧区域表示代码运行的内存结构。当然目前代码已经运行完毕，目前右侧没有显示什么有价值的东西。

如果希望看到代码运行的细节，需要让代码先暂停在某个位置，这里就需要在代码中打一个“断点”，所谓“断点”就是代码停止的位置，只需要在行号上单击即可，再次单击即可取消断点。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-18.png)

​																												*在第7行打断点*



设置断点后，直接刷新页面重新运行代码，此时代码将会停止在设置断点的位置。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-19.png)

​																											*代码停止在第7行*



代码现在停止在了第7行的位置（第7行还没运行），现在我们就可以查看右侧的关于代码的运行细节。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-20.png)



右侧的东西挺多的，我们先看重要的东西。右侧有一个标签叫做Scope，Scope表示区域，可以直接理解为作用域。标签默认是叠起来的，可以单击查看细节。在Scope中显示的就是“传说中”的变量对象。

现在能看到的一个变量对象叫做Global，Global表示全球的全局的。所以这个东西我们也叫做全局对象。在浏览器中全局对象的名字叫做window或globalThis。全局对象很特殊，它是JS中的根对象，JS中的所有一切都存储在它的里边。

像是alert、console这些对象实际都是全局对象的属性。下列三个调用本质上是一样的。

```javascript
alert(123)
window.alert(123)
globalThis.alert(123)
```

所以可以这么理解，全局对象的属性都属于全局变量。但这句话并不意味着所有的全局变量都会存储在全局对象中。现在可以让代码向下执行一下，点击右侧第一行第二个图标，使代码向下执行。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-21.png)

​																														*向下执行代码*



点击按钮后，代码会向下执行一行，也就是执行第7行，第7行代码执行完毕。它的作用是创建一个全局变量a并赋值为10。注意代码执行完毕后，右侧Scope标签下多出了一个Script对象，嗯，没错，这就是全局变量对象。使用let声明的变量全都存储在该对象中，这个对象我们没有办法直接访问，只能通过工具查看。现在可以尝试多声明几个变量，再来查看一下它的结构。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-22.png)

​																												*多声明几个变量*



![img](https://lilichao.com/wp-content/uploads/2020/05/image-23.png)

​																												*查看变量对象*



发现所有的变量都在Script对象中（没有变量的，因为第10行代码还没有执行）。

## 特殊情况

如果使用var关键字声明全局变量，变量会直接添加到全局对象（window）中，不会单独创建Script变量对象。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-24.png)

​																					*使用var声明的全局变量不会创建Script变量对象*



![img](https://lilichao.com/wp-content/uploads/2020/05/image-25.png)

​																										*在global中找到了变量a和b*



使用起来区别不大，但是使用时还是有一些地方比较容易出问题。

```javascript
var a = 10
console.log(window.a) // 10
console.log(globalThis.a) // 10
```

var声明的变量会成为window对象的属性所以上边那么写一点问题也没有。

```javascript
let a = 10
console.log(window.a) // undefined
console.log(globalThis.a) // undefined
```

let声明的变量不会存储到window对象中，使用时会打印undefined

### var的提前声明

除此之外，var声明的变量还有一个特点，它会在所有的代码执行前被声明。比如有如下代码`var a = 10`，变量的声明也就是`var a`会优先执行，通过开发者工具你会发现代码还没执行，但是在window对象中已经具有了a这个属性。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-26.png)

​																													*a被提前声明了*



上例中，第7行代码还未执行，但是在全局对象中已经出现了a这个属性。这就是所谓的提前声明，也可以称为变量的提升。但是此时a的值还是undefined，这是因为只会提前声明并不会提前赋值。

看到这里你会觉得很奇怪，这是什么套路。var关键字本身就是JS早期的产物，并不成熟，所以存在有很多的遗留问题，关于var的特点该了解还是要了解的，但是开发中尽量不要去使用var关键字。

### 函数的提升

除了var声明的变量外，全局中使用function开头的函数也会作为window对象的属性保存，同时也会被提升，并且函数的提升不仅仅是提前声明，所有使用function开头的函数会在所有的代码执行前被创建。

![img](https://lilichao.com/wp-content/uploads/2020/05/image-27.png)



对于函数来说，可以在函数创建前对其进行调用：

```javascript
fn()
 function fn() {
     console.log('我是fn函数')
}
```

上边这么写，一点问题都没有。

```javascript
fn()// 函数没有以function开头，不会提升，这里会报错 
let fn = function () {
     console.log('我是fn函数')
}
fn() // 函数没有以function开头，不会提升，这里会报错
var fn = function () {
    console.log('我是fn函数')
}
```

使用let和var创建函数，不会被提升（var只会提升变量的声明，不会提升函数的创建）。所以在函数声明前调用时会报错。