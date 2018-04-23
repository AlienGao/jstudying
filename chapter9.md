### 类和模块
#### 一个简单地js类
```javascript
// 这个构造函数初始化新创建的“范围对象”
function Range(from, to) {
	this.from = from
	this.to = to
}
// 原型对象定义方法，这些方法为每个范围对象所继承
Range.prototype= {
	constructor: Range, // 显式设置构造函数反向引用
	includes: function(x) {
		return this.from <= x && x <= this.to;
	},
	forEach: function(f) {
		for(var x = Math.ceil(this.from); x <= this.to; x++) {
			f(x)
		}
	},
	toString: function() {
		reutrn this.from + "..." + this.to;
	}
}
```
#### 标准转换方法
```javascript
// toJSON()方法是有JSON。stringify()自动调用。使用JSON.parse()解析时，会得到属性名相同的属性，但是不包含继承来的方法。
var a = {a:1, b:2,c: function(){console.log(1)}}
var b = JSON.parse(JSON.stringify(a))
b // {a: 1, b: 2} 
```
