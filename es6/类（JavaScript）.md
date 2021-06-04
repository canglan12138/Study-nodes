# 类（JavaScript）

类（或构造函数）是一种专门用来创建对象的函数。在早期的JS中，我们需要通过function来定义一个类。但是那种方式并不是十分友好，一来，创建起来会比较的麻烦，需要单独通过原型去添加公共的属性（方法）。二来，它的创建方式和函数太类似不容易区分。

为了解决这个问题，在ES2015中提供新的定义类的语法。新的语法主要有两种书写方式：

```javascript
class name [extends otherName] {
  // class body
}
const MyClass = class [className] [extends otherClassName] {
    // class body
};
```

两种方式效果基本上一致的，有点类似于创建函数的两种方式（函数声明和函数表达式），这里我们以第一种方式为例来定义一个Person类。

```javascript
class Person{
     
}
 
let p1 = new Person();
```

这样我们就定义好了一个Person类，并且可以通过new调用从而创建对象。这种方式本质上和之前通过function创建类的形式是一样的，但这种方式好在明确了我们是在创建一个类，而不是别的什么东西。

## 添加方法

一个空类有什么用呢？我们来看看如何向一个类中添加方法。添加方法非常简单，直接在类中设置即可，语法如下：

```javascript
class name [extends otherName] {
    方法1(){

    }

    方法2(){

    }
}
```

定义方法时不许要使用function关键字，在类中直接设置方法名即可。例如向Person类中添加两个方法run和sleep。

```javascript
class Person{
 
      //定义run方法
      run(){
          console.log('我在跑');
      }
      
      //定义sleep方法
      sleep(){
          console.log('我在睡觉');
      }
 }
 
let p1 = new Person();
p1.run();//调用run方法
p1.sleep(); //调用sleep方法
```

在类中定义的方法会直接设置在原型之中，不需要在手动向原型中添加，这样一来即简化了操作，也避免了创建重复的方法。

## 添加属性

如果需要向示例中添加属性，需要在类中添加一个构造方法constructor，结构如下：

```javascript
constructor(){}
```

constructor意为构造方法，这个方法和其他方法不同，不需要手动调用，而是在创建对象时自动调用，当我们调用类创建对象时，在类内部会自动调用该方法向类中添加属性，可以将需要的属性直接在构造方法中通过this关键字来添加。

修改后类变成如下的样子：

```javascript
class Person {
 
     constructor(name, age, gender) {
         this.name = name;
         this.age = age
         this.gender = gender;
     }
 
     //定义run方法
     run() {
         console.log(`${this.name}在跑`);
     }
 
     //定义sleep方法
     sleep() {
         console.log(`${this.name}在睡觉`);
     }
}
 
let p1 = new Person('孙悟空', 18, '男');
p1.run();
p1.sleep();
```

需要注意的是，如果在构造方法中指定了参数，在创建类时一定要传递这些参数，否则将会导致属性值变成undefined。上述方式和下边的代码是等价的：

```javascript
function Person(name, age, gender){
     this.name = name;
     this.age = age;
     this.gender = gender;
}

Person.prototype.run = function(){
     console.log(`${this.name}在跑`);
}
 
Person.prototype.sleep = function(){
     console.log(`${this.name}在睡觉`);
 }
```

## 静态方法

除此之外，在类中也可以添加静态方法和属性，所谓的静态方法指的是方法或属性可以直接通过类去获取，而无需通过示例，静态方法只需在方法前边添加static关键字即可：

static 方法名(){}
static 属性名=属性值；

示例：

```javascript
class MyClass{
    static a = 'hello'; // 静态属性
    static b(){ // 静态方法
        console.log('我是静态方法');
    }
}
MyClass.a; //调用静态属性
MyClass.b(); //调用静态方法
```