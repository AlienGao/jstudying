### 表达式和运算符
#### 对象和数组的初始化表达式
1.     var a = [1,,,,3]
2.     数组直接量的元素列表结尾处可以留下单个逗号，这时并不会创建一个新的值为undefined的元素。

#### 相等和不等运算符
    0 === -0

#### 比较运算符
1.     对于数字和字符串操作符来说，加号运算符和比较运算符的行为都有所不同，前者更偏爱字符串，如果她的其中一个操作数是字符串的话，则进行字符串连接操作。而比较运算符则更偏爱数字，只有在两个操作数都是字符串的时候，才会进行字符串比较。
2. 	'one' < 3 // false, 'one'被转化为NaN
3. 	'11' < '2' // true,字符串比较
4. 	'11' < 2 // false, 字符串转为数字
5. 	'11' + 3  // 113,数字转为字符串

#### in运算符
1.     var data = [7,8,9]
2.     '0' in data // true:数组包含元素'0'
3.     1 in data // true, 数字转化为字符串
4.     3 in data // false, 数组不包含索引为3的元素

#### 带操作的赋值运算
1.     var a = 1
2.     var data = [1,2,3,4]
3.     data[a++] *= 2  // data = [1,4,3,4]
4.     data[a++] = data[a++] * 2  // data = [1,6,3,4]

#### 全局eval()
    当直接使用非限定的"eval"名称，来调用eval()函数时，通常称为"直接eval"。直接调用eval()时，它总是在调用他的上下文作用域内执行。其他的间接调用则使用全局对象作为其上下文作用域，并且无法读写定义局部变量和函数。
  ```javascript
  var geval = eval;
    var x = 'global', y = 'global';
    function f() {
    	var x = 'local';
    	eval("x += 'changed'")  //直接eval改变局部变量的值
    	return x
    }
    function g() {
    	var y = 'local';
    	geval("y += 'changed'");  //间接调用改变了全局变量的值
    	return y
    }
    console.log(f(), x)    // localchanged global
    console.log(g(), y)   // local globalchanged

```
#### typeof运算符
1.     typeof undefined // 'undefined'
2.     typeof null // 'object'
3.     typeof f // 'function'

#### delete运算符
1.     删除属性或者删除数组元素不仅仅是设置一个undefined的值。当删除一个属性时，这个属性将不再存在。但数组的长度不会改变
2.     delete希望他的操作数是一个左值，如果不是左值，那么delete将不进行任何操作同时返回true。不能删除var语句声明的变量。