### 类型、值和变量摘要
> 当且仅当x为NaN时，表达式 x != x 才成立。
function isNaN(x) {
	return x != x
}

> function isNull(b) {
	return typeof b === 'object' && !b
  // return b === null
}

> function isObject(x) {
	return x.__proto__ === Object.prototype;
}

#### 布尔值
1.     undefined null 0 -0 NaN "" 转化为false
2.     null 转化为数字时为0 undefined转化为数字时为NaN
3. 	所有对象（数组）都会转为true

#### immutable
1.     两个对象包含相同的属性及相同的值，他们也是不想等的。各个索引元素完全相同的两个数组也不相等。
2.     引用类型：当他们都引用同一个基对象时，他们才相等。

#### parseInt()和parseFloat()
1.     如果字符串前缀为'0x'或者'0X'，parseInt()将其解析为十六进制数。parseInt()和parseFloat()都会跳过任意数量的前导空格，尽可能的解析更多数值字符，并忽略后面的内容。如果第一个非空格字符是非法的数字直接量，将最终返回NaN。

#### 对象转换为原始值
1.     对象到原始值的转换基本上是对象到数字的转换（首先调用valueOf()），日期对象则使用对象到字符串的转换模式。通过valueOf()和toString()返回的原始值将被直接使用，而不会被强制转换为数字或字符串。
2.     new Date() == new Date().toString()     // true
3.     new Date() ==  new Date().valueOf()    // false

#### 作为属性的变量
1.     当使用var声明一个变量时，创建的这个属性是不可配置的，也就是说这个变量无法通过delete运算符删除。

#### 作用域链
1.     每次调用外部函数的时候，作用域链都是不同的。