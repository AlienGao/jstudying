### 函数
#### 反法调用
嵌套函数不会调用对他的函数继承this，其this值不是全局对象（非严格模式下）就是undefined（严格模式下）。
```javascript
var o = {
	m: function() {
		var self = this;
		console.log(this === o) // true
		f()
		function f() {
			console.log(this === o) // false, this指代window
			console.log(self === o) // true, self指代外部函数的this
		}
	}
}
```
#### callee属性
```javascript
// 通过callee来递归调用自身
var factorial = function (x) {
	if(x <= 1) return 1;
	return x * arguments.callee(x -1);
}
```
#### 将对象属性用做实参
```javascript
// 不用按照形参顺序传参
function easycopy(args) {
	arraycopy(args.from, args.from_start || 0, args.to, args.to_start || 0, args.length)
}
var a = [1, 2, 3], b = {};
easycopy({from: a, to: b, length: 4})

```
#### 判断实参类型，尽可能的将之前非数字转化为数字求和
```javascript
function flexsum(x) {
	var total = 0;
	for(var i = 0; i < arguments.length; i++) {
		try{
			var element = arguments[i]
			if(element == null) continue // 忽略null和undefined实参
			if(Array.isArray(element)) {
				n = flexsum.apply(this, element)
			} else if (typeof element === 'function') {
				n = Number(element())
			} else {
				n = Number(element)
			}
			if(isNaN(n)) {
				throw Error("flexsum() can't convert " + element + " to number");
			}
		} catch (e) {
			console.log(e);
			continue;
		}
		total += n
	}
	return total;
}
```
#### 自定义函数属性
```javascript
// 当函数需要一个“静态”变量来在调用时保持某个值不变，最方便的方式就是给该函数定义属性。
function factorial(n) {
	if(isFinite(n) && n > 0 && n === Math.round(n)) {
		if(!(n in factorial)) {
			factorial[n] = n * factorial(n - 1)
		}
		return factorial[n]
	} else {
		return NaN
	}
}
factorial[1] = 1 // 初始化缓存
```
#### 闭包
```javascript
// 嵌套函数f()定义在这个作用域链里，其中的变量一定是局部变量，不管何时何地执行f()，这种绑定在执行f()时依然有效。
var a = 'global'
 function check(){
	var a = 'local'
	function f() {return a}
	return f
}
cheak()()  // 'local'
```