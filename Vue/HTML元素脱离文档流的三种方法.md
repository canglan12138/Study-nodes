# [HTML元素脱离文档流的三种方法](https://www.cnblogs.com/ning123/p/11011845.html)

## 一、什么是文档流？

将窗体自上而下分成一行一行，并在每行中按从左至右依次排放元素，称为文档流，也称为普通流。

这个应该不难理解，HTML中全部元素都是盒模型，盒模型占用一定的空间，依次排放在HTML中，形成了文档流。

## 二、什么是脱离文档流？

元素脱离文档流之后，将不再在文档流中占据空间，而是处于浮动状态（可以理解为漂浮在文档流的上方）。

脱离文档流的元素的定位基于正常的文档流，当一个元素脱离文档流后，依然在文档流中的其他元素将忽略该元素并填补其原先的空间。

## 三、怎么脱离文档流？

### 1：float

使用float脱离文档流时，其他盒子会无视这个元素，但其他盒子内的文本依然会为这个元素让出位置，环绕在该元素的周围。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .first {
            width: 200px;
            height: 200px;
            border: 3px solid red;
            float: left;
        }
        .second {
            width: 200px;
            height: 100px;
            border: 3px solid blue;
        }
    </style>
</head>
 
<body>
 
<div class="first">123</div>
<div class="second">456</div>
 
</body>
</html>
```

运行效果：

![img](https://img2018.cnblogs.com/blog/1022714/201906/1022714-20190612193652970-261445832.png)

 

这段代码中把红色的框设置为了左浮，所以红色的框称为了浮动状态（浮动在蓝色框的上面），而蓝色框占用了原来红色框的位置。

注意到，蓝色框中的文本依然认为红色框存在，所以为红色框让出了位置。

由于div是块状元素，所以456出现在下方。

 

### 2：absolute

absolute称为绝对定位，觉得应该称为相对定位，

因为使用absolute脱离文档流后的元素，是相对于该元素的父类（及以上，如果直系父类元素不满足条件则继续向上查询）元素进行定位的，

并且这个父类元素的position必须是非static定位的（static是默认定位方式）。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .first {
            width: 200px;
            height: 200px;
            border: 3px solid red;
        }
        .second {
            width: 200px;
            height: 100px;
            border: 3px solid blue;
            position: absolute;
        }
        .third {
            width: 200px;
            height: 200px;
            border: 3px solid green;
        }
    </style>
</head>
 
<body>
 
<div class="first">123</div>
<div class="second">456</div>
<div class="third">789</div>
 
</body>
</html>
```

运行效果：

![img](https://img2018.cnblogs.com/blog/1022714/201906/1022714-20190612194530452-2031081250.png)

通过把蓝色的框的position设置为absolute使蓝色的框变为浮动状态，可以看到绿色的框被蓝色的框遮挡。

emmm...，看起来貌似没有问题，但是还记得前面说的absolute是相对谁定位的吗？

相对非static元素的父级定位的，这里蓝框的父级就是html，所以应该是相对于html定位，

但是代码中没有提供相对位置，所以只能浮动在原来该元素在文档流中的位置上方。



### 3：fixed

完全脱离文档流，相对于浏览器窗口进行定位。（相对于浏览器窗口就是相对于html）。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .first {
            width: 200px;
            height: 200px;
            border: 3px solid red;
        }
        .second {
            width: 200px;
            height: 100px;
            border: 3px solid blue;
            position: fixed;
            right: 0;
            top: 0;
        }
        .third {
            width: 200px;
            height: 200px;
            border: 3px solid green;
        }
        html {
            border: dotted;
        }
    </style>
</head>
 
<body>
 
<div class="first">123</div>
<div class="second">456</div>
<div class="third">789</div>
 
</body>
</html>
```

![img](https://img2018.cnblogs.com/blog/1022714/201906/1022714-20190612194826550-1024434166.png)

 

 可以很明显的看出，蓝色的框是相对于html进行定位的。

如果不提供相对位置的话，蓝色的框会浮动在其原先在文档流中的位置上方。

 