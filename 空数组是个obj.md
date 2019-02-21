#### 空数组是个obj
<http://bbs.csdn.net/topics/390867114>

<http://blog.csdn.net/q617610589/article/details/56958947>

	var arr = []
	typeof arr;  // "object"
	
	if(arr)console.log("it's true");  // it's true
	
	arr == false; // true
	arr == true; // false
	Boolean(arr); // true
	Number(false)  // 0
	Number(arr)  // 0
	
**任意值与布尔值比较，都会将两边的值转化为Number。** 


##### apply 和call
<http://blog.jobbole.com/77496/>