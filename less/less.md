```less
// less中的单行注释，注释中的内容不会被解析到css中

/*
    css中的注释，内容会被解析到css文件中
*/
.box1{
    background-color: #bfa;

    .box2{
        background-color: #ff0;

        .box4{
            color: red;
        }
    }

    .box3{
        background-color: orange;
    }
  //子元素写法
  & > .son {
    background: yellow;
  }
}

//变量，在变量中可以存储一个任意的值
// 并且我们可以在需要时，任意的修改变量中的值
// 变量的语法： @变量名
@a:200px;
@b:#bfa;
@c:box6;

.box5{
    //使用变量是，如果是直接使用则以 @变量名 的形式使用即可
    width: @a;
    color:@b;
}

//作为类名，或者一部分值使用时必须以 @{变量名} 的形式使用
.@{c}{
    width: @a;
    background-image: url("@{c}/1.png");
}

@d:200px;
@d:300px;

div{
    // 变量发生重名时，会优先使用比较近的变量
    @d:115px;
    width: @d;
    height: @e;
}

//可以在变量声明前就使用变量
@e:335px;


div{
    width: 300px;
    // 新版的语法
    // height: $width;
}

```

```less
.box1{
    .box2{
        color: red;
    }

    >.box3{
        color: red;

        &:hover{
            color: blue;
        }
    }

    //为box1设置一个hover
    //& 就表示外层的父元素
    &:hover{
        color: orange;
    }

    div &{
        width: 100px;
    }
}

.p1{
    width: 100px;
    height: 200px;
}

//:extend() 对当前选择器扩展指定选择器的样式（选择器分组）
.p2:extend(.p1){
    color: red;
}

.p3{
    //直接对指定的样式进行引用，这里就相当于将p1的样式在这里进行了复制
    //mixin 混合
    .p1();
}

// 使用类选择器时可以在选择器后边添加一个括号，这时我们实际上就创建了一个mixins
.p4(){
    width: 100px;
    height: 100px;
}

.p5{
    .p4;
}

//混合函数 在混合函数中可以直接设置变量
.test(@w:100px,@h:200px,@bg-color:red){
    width: @w;
    height: @h;
    border: 1px solid @bg-color;
}

div{
    //调用混合函数，按顺序传递参数
    // .test(200px,300px,#bfa);
    .test(300px);
    // .test(@bg-color:red, @h:100px, @w:300px);
}

span{
    color: average(red,blue);
}

html{
    width: 100%;
    height: 100%; 
}
body {
    width: 100%;
    height: 100%;
    background-color: #bfa;
}

body:hover{
    background-color: darken(#bfa,50%);
}
```

```less
//import用来将其他的less引入到当前的less
//可以通过import来将其他的less引入到当前的less中
@import "syntax2.less";

.box1{
    // 在less中所有的数值都可以直接进行运算
    // + - * /
    width: 100px + 100px;
    height: 100px/2;
    background-color: #bfa;
    
}

```

