### 对象
#### Object.create()
```javascript
// inherit()函数的一个用途是防止库函数无意间修改那些不受你控制的对象。当函数读取继承对象的属性时，实际上读取的是继承来的值。如果给继承对象的属性赋值，则这些属性只会影响这个继承对象自身，而不是原始对象。
function inherit(p) {
	if(p == null) return TypeError;
	if(Object.create) 
		return Object.create(p)
	var t = typeof p
	if(t !== 'object' && t !== 'function') {
		throw TypeError
	}
	function f() {}
	f.prototype = p
	return new f()
}
```
#### 枚举属性
```javascript
// 把p中的可枚举属性复制到o中，并返回o。如何含有同名属性，则覆盖o
function extend(o, p) {
	for (x in p) {
		o[x] = p[x]
	}
	return o
}
```
```javascript
// 将p中的可枚举属性复制到o中，并返回o。如果两者含有同名属性，o中的属性不受影响。
function merge(o, p) {
	for(x in p) {
		if(o.hasOwnProperty(x)) continue;
		o[x] = p[x]
	}
	return o
}
```
```javascript
// 如果o中的属性在p中没有同名属性，则删除o中的这个属性
function restrict(o, p) {
	for(x in o) {
		if(!p.hasOwnProperty(x)) {
			delete o[x]
		}
	}
	return o
}
```
```javascript
// 如果o中的属性在p中存在同名属性，则从o中删除这个属性
function subtract(o, p) {
	for(x in p) {
		delete o[x]
	}
	return o
}
```
```javascript
// 返回一个新对象，这个对象同时拥有o和p的属性。如果o和p中有重名属性，则使用p中属性
function union(o, p) {
	return extend(extend({}, o), p)
}
```
```javascript
// 返回一个新对象，该对象同时拥有o的属性和p的属性
function intersection(o, p ) {
	return restrict(extend({}, o), p);
}
```
```javascript
// 返回一个数组，这个数组包含的是o中可枚举的自有属性名称
function keys(o) {
	if(typeof o !== 'object') throw TypeError()
	const result = []
	for (x in o) {
		if(o.hasOwnProperty(x)) {
			result.push(x)
		}
	}
	return result
}
```
#### 属性的getter和setter
```javascript
var p = {
	x: 1.0,
	y: 1.0,
	// r是可读写的存取器属性，他有getter和setter
	get r() {
		return Math.sqrt(this.x * this.x + this.y * this.y)
	},
	set r(newValue) {
		var oldValue = Math.sqrt(this.x * this.x + this.y * this.y)
		var radio = newValue / oldValue
		this.x *= radio
		this.y *= radio
	},
	get theta() {
		return Math.atan2(this.y, this.x)
	}
}
// 和数据属性一样，存取器属性也是可以继承的。
```
```javascript
// 复制属性的特性
// 给Object.property添加一个不可枚举的extend()方法，这个方法继承自调用他的对象，将作为参数传入的对象的属性一一复制。
Object.defineProperty(Object.property, 'extend', {
	writable: true,
	enumerable: false,
	configurable: true,
	value: function(o) {
		var names = Object.getOwnPerprotyNames(o)
		for(var i = 0; i < names.length; i++) {
			if (names[i] in this) continue;
			var desc = Object.getOwnPerprotyDescriptor(o, names[i]);
			Object.defineProperty(this, names[i], desc);
		}
	}
})
```
#### 类属性
```javascript
// 获取一个对象的类
function classof (o) {
	if(o === null) return null;
	if(o === undefined) return undefined
	return Object.prototype.toString.call(o).slice(8, -1)
}
```