### 数组
#### 数组创建
> 数组直接量的语法允许有可选的结尾的逗号，故[,,]只有两个元素而非三个。

#### 数组遍历
> for/in 循环能够枚举继承的属性名，如添加到Array.prototype中的方法。由于这个原因，在数组上不应该使用for/in循环，除非使用额外的检测方法来过滤不想要的属性。

```javascript
for(var i in a) {
	if(!a.hasOwnproperty(i)) continue;
}
for (i in a) {
	if(String(Math.floor(Math.abs(Number(i)))) !== i) continue;
}
```
#### 多维数组
```javascript
// 九九乘法表
var table = new Array(10)
for (var i = 0; i < table.length; i++) {
	table[i] = new Array(10)
}
for(var row = 0; row < table.length; row++) {
	for(var col = 0; col < table[row].length; col++) {
		table[row][col] = row * col
	}
}
```
#### 数组的方法
1. 改变原数组： reserve() splice() sort() splice() **（返回一个删除元素组成的数组）** push() pop() unshift() shift() **(当使用多个参数调用unshift时，参数是一次性插入的，而非一次一个的插入。这意味着最终数组插入的元素的顺序和他们在参数列表中的顺序表现一致)** reduce() every() some() 
2. 创建并返回一个新数组： concat() slice()  **（返回指定的数组片段或子数组）** map() **（map返回的是新数组，如果是稀疏数组，返回的也是相同的稀疏数组）** filter() **(filter会跳过稀疏数组中求缺少的袁术，他返回的数组总是稠密的)**
#### 类数组对象
```javascript
// 类数组对象没有继承自Array.prototype,那就不能在他们上面直接调用数组方法，但是可以间接的使用Function.call方法调用
var a = {'0': 'a', '1': 'b', '2': 'c', length: 3}
Array.prototype.join.call(a, '+') // "a+b+c"
Array.prototype.map.call(a, function(x){
	return x.toUpperCase();
}) // ["A", "B", "c"]
```