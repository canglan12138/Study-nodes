# for in 与普通 for 的比较

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>

	<script>
		window.onload = () => {
      var pAll = document.getElementsByTagName('p')

      /*
			* 键：0          键的类型：string
			* 键：1          键的类型：string
			* 键：length     键的类型：string
			* 键：item       键的类型：string
			* 键：namedItem  键的类型：string
			*/
			for (let key in pAll) {
        console.log('键：' + key + '   ' + '键的类型：' + typeof key + '   ' + '值：' + key.value);
      }
      console.log('--------------------');
      console.log(pAll);

      /*
      *	 0 number
      *  1 number
      * */
			for (let i = 0;i < pAll.length;i++) {
        console.log(i + ' ' + typeof i);
      }
		}
	</script>
</head>
<body>

<p>123</p>
<p>456</p>

</body>
</html>

```

![image-20210413125420325](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210413125420325.png)

从图上可以看出，for..in循环会把某个类型的原型(prototype)中方法与属性给遍历出来，for…in循环中的循环计数器是字符串，而不是数字