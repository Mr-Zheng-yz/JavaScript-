## 一、数据类型

### Number
JavaScript不区分整数和浮点数，统一用Number表示。

> NaN；//NaN表示Not a Number，当无法计算结果时用NaN表示。
> Infinity;//Infity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示Infinity.

### 字符串
字符串是以单引号或双引号括起来的任意文本，比如'abc',"xyc"。

#### 转义字符
如果字符串中包含`'`，又包含`"`，可以是使用转义字符`\`来标识。如
```
“I\'m \"OK\"!”; //内容是I'm "OK"!
```
转义字符\可以转义很多字符，比如\n表示换行，\t表示制表符，字符\本身也要转义，所以\\表示的字符就是\。

ASCII字符可以以\x##形式的十六进制表示，如:
```
'\x41; // 完全等同于'A'`
```
还可以用\u####标识一个Unicode字符：
```
'\u4e2d\u6587'; //完全等同于'中文'
```

#### 多行字符串
最新的ES6标准新增了一种多行字符串的表示方法，用反引号 `...` 表示：
```
`这是一个
多行
字符串`
```
如果浏览器不支持ES6标准，请把多行字符串用\n重新表示出来。

#### 模板字符串
1. 使用` + `连接多个字符串。
2. ES6标准，使用模板字符串。表示方法和多行字符串一样，但它会自动替换${}中的变量，如：
```
var name = “小明”;
var age = 20;ß
var message = `你好，${name},你今年${age}岁了`；
alertmessage);
```

#### 操作字符串
1. 获取字符串长度：`s.length;`
2. 获取字符串指定位置的字符，使用类似Array的下标操作，索引从0开始。
```
var a = “Hellow,world;”
a[0]; // H
```
***特别注意***：字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但也没有任何效果。

3. 字符串函数：
 * toUpperCase：把一个字符串全部变为大写。
 * toLowerCase：把一个字符串全部变为小写。
 * indexOf：搜索指定字符串出现的位置。
 * substring： 返回指定索引区间的子字符串。

```
var s = “Hellow”;
s.toUpperCase(); // HELLOW
s.toLowerCase(); // hellow
s.indexOf(“he”); // 返回0
s.substring(0,5); // hello 从索引0到5(不包括5)
```
***注意：这些函数并没有改变原有字符串，而是返回了一个新字符串。***

### 布尔值
一个布尔值只有true、false两种值。

### null和undefined
null表示"空",undefined表示"未定义"。
大多数情况下都应该使用null。undefined仅仅在判断函数参数是否传递的情况下有用。

### 数组
数组是一组按顺序排列的集合，集合的每个值称为元素。JavaScript的数组可以包括任意数据类型。
数组用[ ]表示，元素之间用,分隔。如：
```
[1,2,3.14,'hellow',null,true]
```
另一种穿件数组的方法是通过Array()函数实现。
```
new Array(1,2,3);
```
建议直接使用[ ];
数组元素可以通过索引来访问，首个元素下标从0开始。

***注意：要取得Array长度，直接访问length属性。如果直接给Array的length赋一个新的值，会导致Array大小的变化。***
```
var arr = [1,2,3];
arr.length; // 3
arr.length = 6; // arr变为[1, 2, 3, undefined, undefined, undefined]
```

***注意：如果通过索引赋值，，如果索引超过了length范围，同样会引起Array大小变化。***
```
var arr = [1,2,3];
varr[4] = 4; // arr变为1,2,3，undefined，4
```

#### 数组操作函数
1. indexOf()：搜索一个指定元素的位置。
```
var arr = [10,20,'30','xyc'];
arr.index(10); // 返回0
```

2. slice():截取Array的部分元素，返回一个新的Array。对应String的substring()；
* slice()的起止参数包含开始索引，不包括结束索引。
* 如果不传任何参数，就截取所有元素，可以利用这一点复制一个Array。
```
var arr = ['A','B','C','D','E','F'];
arr.slice(0,3); // 返回['A','B','C']
```


3. push()和pop()
* push():向Array的末尾添加若干元素。返回push()后数组长度。
* pop():把Array的最后一个元素删除掉。返回被删除元素。
***注意：空数组继续pop不会报错，而是返回undefined，修改的都是原数组。***

4. unshift和shift
* unshift():向Array的头部添加若干元素。
* shift():把Array的第一个元素删掉。
注意事项同上面的push()和pop();

5. sort():对当前Array进行排序，会直接修改但该案Array的元素位置，按默认顺序排序。
```
var arr = ['B', 'C', 'A'];
arr.sort(); // ['A', 'B', 'C']
```

6. reverse()：把整个Array的元素反转。
```
var arr = ['one', 'two', 'three'];
arr.reverse(); // ['three', 'two', 'one']
```

7. splice():是修改Array的万能方法，可以从指定索引开始删除若干元素，然后从该位置添加若干元素。返回值是被删除元素。
```
参数1：指定索引位置；参数2：删除元素个数；参数3~n：要添加的元素；
var arr1 = ["A","B","C"];
arr1.splice(1,2,"C","D"); // 返回["B","C"],原数组变为["A","C","D"]
```

8. concat()：把当前Array和另一个Array连接起来，并返回一个新的Array。
```
var arr = ["A","B","C"];
var arr2 = [1,2];
var added = arr.concat(arr2);//返回["A","B","C",1,2]

```
*** 注意：concat()方法可以接收任意个元素和Array，并自动把Array类型参数拆开，全部添加进新的Array。***
```
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```

9. join()：把当前Array的每个原始都用指定的字符串连接起来，然后返回连接后的字符串。比较实用。
```
var arr = ["A","B","C",1,2,3];
arr.joing("-"); // 返回"A-B-C-1-2-3“
```

#### 多维数组
如果数组的某个元素又是一个数组，则可以形成多维数组。
```
var arr = [[1, 2, 3], [400, 500, 600], '-'];
arr[1][1]; // 返回500
```


### 对象
JavaScript的对象是一组由键-值组成的无序组合。
```
var person = {
    name:'bob',
    age:20,
    tags:['js','web','mobile'], 
    hasCar:true
};

```
* 语法：用一个`{...}`表示一个对象，键值对以`xxx:xxx`形式声明，用`,`隔开。
* JavaScript对象的键都是`字符串`类型，值可以是`任意数据类型`。
* 要获取一个对象的属性， 用**对象变量.属性名**的方式，通过这种方式要求属性名必须是一个有效的变量名。
* 如果属性名不是有效变量名，声明时需要用`''`括起来。访问时通过**对象变量['属性名']**的方式。
```
var xiaohong = {
    name: '小红',
    'middle-school': 'No.1 Middle School'
};
xiaohong['middle-school'];//访问无效变量对应值
xiaohong['name']与xiaohong.name都能访问有效变量。
```
***注意：访问不存在的属性不会报错，而是返回undefined***

#### 动态为对象添加和删除属性
* 添加属性：直接访问对象属性并赋值即可。**对象变量.属性名 = 赋的值**
* 删除属性：delete关键字。**delete 对象变量['属性名']**
```
var xiaoming = {
    name: '小明'
};
xiaoming.age;// undefined
xiaoming.age = 18; // xiaoming有了age属性，值为18
delete xiaoming.age; //xiaoming没有age属性了，变为undefined
delete xiaoming['name']; //另一种访问，name属性为undefined
delete xiaoming.school；//删除一个不存在的属性不会报错
```

#### `in`操作符
检测对象是否存在某一属性。继承得到的也会被认为这个属性存在。**属性名 in 对象名**
```
var xiaoming = {
	name:"小明“
};
'name' in xiaoming;// 返回 true
'grade' in xiaoming; // 返回false
'toString' in xiaoming; //返回true，toString定义object中,所有对象都继承object。
```

#### `hasOwnProperty()`方法
判断一个属性是否是这个对象自身定义的。**对象名.hasOwnProperty(属性名);**
```
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```


### Map和Set

#### Map
ES6引入了新的数据类型`Map`，Map是一组键值对结构。
* Map的初始化：
1. 直接使用二维数组赋值并初始化。
2. 初始化一个空的Map。
```
var m = new Map([['yanze',100],['mingzhu',99]]);//
var m = new Map();
```

#### Map操作函数
1. set(key,value)：添加新的key-value
2. has(key)：判断是否存在key
3. get(key)：//获取key对应value
4. delete(key)：//删除key-value

* 获取一个不存在的key返回undefined。
* 一个key只能对应一个value，多次对一个key放入value，后存放会替换先存放的。

#### Set
Set是一组key的集合，但不存放value。并且在Set中没有重复的key。

* Set的初始化：
1. 使用Array初始化Set。
2. 初始化空的Set。
```
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```

#### Set操作函数
1. add(key)：添加一个元素。
2. delete(key)：删除一个元素。
```
var s = new Set([1, 2, 3]);
s.add(4); // {1,2,3,4}
s.delete(4); // {1,2,3}
```
* 重复元素在Set中会自动被过滤。

### iterable类型
ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。

#### `for ... of`遍历iterable类型
语法：for(var 值 of iterable类型变量 ){ }
```
var arr = [1,2,3];
for(var a of arr){}
```

* `for...of` 与 `for...in` 区别：
for...in：遍历的是对象的属性，如果个一个Array加上一个属性，那么可能会将这个属性也遍历出来，尽管Array本身没有这个舒心。
for...of: 只循环集合本身的元素。

因此，遍历一个集合最好用`for...of方法`，前提是浏览器支持ES6标准。

#### iterable内置的`forEach()`方法：
接收一个函数，每次迭代就自动回调该函数。

* `Array`：
```
var a = ['A','B','C'];
a.forEach(function(element,index,array){
	// element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
```

* `Set`：Set没有索引，所以回调函数的前两个参数都是元素本身。
```
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    console.log(element);
});
```

* `Map`：Map的回调函数参数依次为：value、key和Map本身。
```
var m = new Map([1,'x'],[2,'y'],[3,'z']);
m.forEach(function(value,key,map){
	console.log(value);
});
```


##二、基本语法

###条件判断
关键字有`if`、`else if`和`else`关键字，用法与java一样。
*** 注意：JavaScript把null、undefined、0、NaN和空字符串''视为false，其他值一概视为true***

###循环

#### for循环
基本使用：
```
var x = 1;
for(var i = 2;i <= 10;i++){
    x = x * i;
}
//计算阶乘：1 x 2 x 3 x ... x 10 = 3628800
```
遍历数组。

* 变体：`for...in`，可以把一个对象的所有属性依次循环出来。
语法：for(var key in 对象变量){ key 为属性名 }
```
var o = {
	name:'jack',
	age:20,
	city:"Beijing"
};
for(var key in o){
	console.log(key); // name,age,city
	//配合hasOwnProperty()可以过滤掉对象继承的属性。
	if(o.hasOwnProperty(key)){
		console.log(key);
	}
}
```

* `for...in`循环可以直接循环出Array的索引
```
var a = ['A', 'B', 'C'];
for (var i in a) {
    console.log(i); // '0', '1', '2'
    console.log(a[i]); // 'A', 'B', 'C'
}
```
***注意：`for ... in`对Array的循环得到的是String而不是Number。***

#### `while`循环和`do ... while`
`do ... while`和`while`循环的唯一区别在于，不是在每次循环开始的时候判断条件，而是在每次循环完成的时候判断条件



### 变量
申明一个变量用var语句，如：
```
var a;// 申明了变量a，此时a的值为undefined
var $b = 1; // 申明了变量$b，同时给$b赋值，此时$b的值为1
```

特点：可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量，但是要注意只能用var申明一次

### 比较运算符
1. ==比较：会自动转换数据类型再比较，很多时候，会得到非常诡异的结果。
2. === 比较：不会自动转换数据类型，如果数据类型不一致，返回false，如果一致，再比较。

因此不要使用==比较，始终坚持使用===比较。

#### 例外的NaN：
NaN这个特殊的Number与所有其他值都不相等，包括他自己。唯一能判断NaN的方法是通过isNaN()函数。
```
Nan === NaN; // false
isNaN(NaN); //true
```

#### 浮点数的相等比较：
浮点数在运算过程中会产生误差，因为计算机无法精确表示无限循环小舒。要比较两个浮点数是否相等，
智能计算它们之间的绝对字号，看是否小于某个阙值。
```
1 / 3 === (1 - 2 / 3); //false 
Math.abs(1 / 3 -( 1- 2 / 3)) < 0.00000001; //true
```

### strict模式
* JavaScript在设计之初，并不强制使用`var`申明变量，如果没有通过`var`申明就被使用，那么该变量就自动被申明为全局变量。如：
```
i = 10; // i现在是全局变量
```

* 独立函数中，strict模式下，`this`指向undefined;非strict模式下，`this`指向window。

#### 作用
在strict模式下运行的JavaScript代码，强制通过`var`申明变量，未使用var申明变量就使用的，将导致运行错误。

#### 开启方法
启用strict模式的方法是在JavaScript代码的第一行写上:
```
'use strict'；
```
不支持的浏览器会把它当做一个字符串语句，支持strict的浏览器会开启strict模式运行JavaScript.

## 三、函数

###定义函数的方式：
方式一：. function 函数名称(参数){ 函数体 }
```
function abs(x){
	if(x>=0){
		return x;
	}else{
		return -x;
	}
}
```

方式二：var 函数名 = function(参数){ 函数体 }
```
var abs = function(x){
	if(x>=0){
		return x;
	}else{
		return -x;
	}
};
```

这种方式下，function (x) { ... }是一个匿名函数，它没有函数名。但是，这个匿名函数赋值给了变量abs，所以，通过变量abs就可以调用该函数。

* JavaSctipt允许传入人一个参数而不影响使用。
```
abs(10);//返回10
abs(10,“哈哈哈”);//返回10
abs();// x参数将接收到undefined，计算结果为NaN
```
* 如果没有`return`语句，函数执行完会返回`undefined`。

* 可以通过`typeof`关键字检查参数类型。
```
if (typeof x !== 'number') {
    throw 'Not a number';
}
```

### `arguments`关键字
只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。

* `arguments`用法相当于一个Array。
```
function foo(x) {
    console.log('x = ' + x); // 只拿到传入的第一个参数，10 
    for (var i=0; i<arguments.length; i++) {
        console.log('arg ' + i + ' = ' + arguments[i]); // 10, 20, 30
    }
}
foo(10,20,30);
```

### `rest`参数
`rest`参数是ES6标准引入的，可以获取额外传入参数。
`rest`参数只能写在最后，前面用`...`标识。
```
function foo(a,b,...rest){}
```

* rest是Array类型参数。
* 如果传入的正常定义参数都没填满，rest参数会接收一个空数组而不是undefined。

### 变量作用域
* 不同函数内部的同名变量互相独立，互不影响；
* 内部函数可以访问外部函数定义的变量，反过来则不行；
* 如果内部函数定义了与外部函数重名的变量，则内部函数的变量将“屏蔽”外部函数的变量。

#### 变量提升
1. JavaScript函数会先扫描整个函数体的语句，把所有声明的变量"提升"到函数顶部。
2. JavaScript引擎虽然提升了变量的声明，但不会提升变量的赋值。
```
function foo(){
  var x = 'Hellow,' + y;
  console.log(x);// 不会报错，显示Hellow，undefined，证明了上面变量提升的第二点。
  var y = 'bob';
}
```

#### 全局作用域
JavaScript默认有一个全局对象`window`，全局作用域的变量实际上被绑定到`window`的一个属性。
```
var couse = 'Learn JavaScript';
alert(couse);// 'Learn JavaScript';
alert(window.couse);// 'Learn JavaScript';
```
直接访问全局变量course和访问window.course是完全一样的。

* 以变量方式定义的函数实际上也是一个全局变量(var foo = function(){})。
```
function foo() {
    alert('foo');
}
foo(); // 直接调用foo()
window.foo(); // 通过window.foo()调用
```

总结：JavaScript实际上只有一个全局作用域。任何变量如果没在当前函数作用域中找到，就会继续向上查找，如果在全局作用域也没找到，则报`ReferenceError`错误。

#### 名字空间
全局变量会绑定到`window`上，不同的JavaScript如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突，并且很难被发现。
实际开发中建议把自己的所有变量和函数全部绑定到一个全局变量中。
```
var MYAPP = {};//唯一的全局变量
MYAPP.name = 'myapp';
MYAPP.version = 1.0;
//函数
MYAPP.foo = function(){  
	return 'foo';
}
```
把自己的代码全部放入唯一的名字空间MYAPP中，会大大减少全局变量冲突的可能。

#### 局部作用域：`let`关键字
* 问题：在for循环等语句块中是无法定义具有局部作用域变量的：
```
function foo(){
	for(var i=0;i<100;i++){
		...
	}
	i += 100;//仍然可以引用变量
}
```
为了解决块级作用域，ES6引入了新的关键字`let`，用`let`替代`var`可以申明一个块级作用域变量：
```
function foo(){
	for(let i=0;i<100;i++){
		...
	}
	i += 100;//SyntaxError
}
```

### 常量
ES6标准引入了新的关键字const来定义常量。
`const`与`let`都具有块级作用域：
```
const PI = 3.14;
PI = 3;//某些浏览器不报错，但是无效果
PI;//3.14
```

### 解构赋值
ES6开始引入了解构赋值，可以同时对一组变量进行赋值。
* 对数组元素进行解构赋值时，多个变量要用`[...]`括起来。
```
var [x,y,z] = ['Hellow','JavaScript','ES6'];
x;// Hellow
y;//JavaScript
z;//ES6
```

* 如果数组还有嵌套，那么变量组也要有嵌套，注意嵌套层次和位置要保持一致。
```
let [x,[y,z]] = ['Hellow',['JavaScript','ES6']]
x;//Hellow
y;//JavaScript
z;//ES6
```

* 解构赋值还可以忽略某些元素。
```
let[,,z] = ['Hellow','JavaScript','ES6'];
z;//ES6
```

#### 对象的解构赋值
* 语法：var/let {属性名...} = 对象;
```
var person = {
	name:'小明’,
	age；20
};
var {name,age} = person;
```

* 同样可以直接对嵌套的对象属性进行赋值，只要保证对应的层次是一致的：
```
var person = {
	name:'小明',
	age:20,
	address:{
		city:'Beijing',
		zipcode:'10001
	}
};
var {name,address:{city,zip}} = person;
name;//小明
city;//Beijing
zip;//undefined,因为属性名是zipcode而不是zip
//注意：address不是变量，而是为了让city和zip获取嵌套的address对象属性
address;//Uncaught ReferenceError: address is not defined
```

***注意：若对应的属性不存在，变量将被赋值为`undefined·***

* 要使用的变量名和属性名不一致的赋值语法：
语法：var/let {属性名:要使用的变量名} = 对象；
```
var person = {
	name:'小明',
	passport: 'G-12345678',
};
//把passport赋值给id
let {name,passport:id} = person;
name;//小明
id；//'G-12345678'
//注意：passport不是变量，而是为了让id获取passport属性。
passport;//Uncaught ReferenceError: address is not defined
```

* 解构赋值还可以使用默认值，避免不存在的属性返回`undeined`问题
```
var person = {
	name:'小明',
	age:20
};
//如果person对象没有single属性，默认赋值为true
var {name,single=true} = person;
name;//小明
single;//true
```

* 如果变量已经被声明了，再次赋值的时候，正确的写法也汇报语法错误：
```
var x,y;
{x,y} = {name:'小明',x:100,y:200}
// 语法错误: Uncaught SyntaxError: Unexpected token =
```
因为JavaScript引擎把`{`开头的语句当做了块处理，于是`=`不再合法。(语句块不能赋值)
解决方法是用小括号将语句括起来。
```
({x, y} = { name: '小明', x: 100, y: 200});
```

#### 使用场景

1. 交换两个变量`x`和`y`的值:
```
var x = 1,y=2;
[x,y] = [y,x]
```

2. 快速获取当前页面的域名和路径
```
var {hostname:domain,pathname:path} = name;
```

3. 如果一个函数用对象作为参数，那么，可以使用解构直接把对象的属性绑定到变量中,并且可以设置默认值：
```
//使用匿名对象当做参数，这时可以直接使用它的属性名作为变量
function buildDate({year,month,day,hour = 0,minute = 0,second = 0}){
	return new Date(year + '-" + month + '-' + day + ' ' + hour + ':' + minute + ':' + second);
}
//参数同样为对象,可以只传入year、mouth和day：
buildDate({year:2017,mouth:1,day:1});//Sun Jan 01 2017 00:00:00GMT+0800(CST)

//也可以传入hour、minute和second：
buildDate({year: 2017, month: 1, day: 1, hour: 20, minute: 15 }});// Sun Jan 01 2017 20:15:00 GMT+0800 (CST)

```

### 方法

#### `this`关键字
在一个方法内部，this是一个特殊变量，它始终指向当前对象。
```
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;
    }
};
xiaoming.age; // function xiaoming.age()
xiaoming.age(); // 今年调用是25,明年调用就变成26了
```

* 在一个独立函数中使用`this`关键字，非stict模式指向的是`window`，stict模式指向undefined。
```
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};
xiaoming.age(); // 25, 正常结果
getAge(); // NaN
```

* 要保证`this`指向正确，必须用`obj.xxx()`的形式调用。

* 在对象的函数内部的函数，`this`又指向了undefined。（在非strict模式下，它重新指向全局对象window！）
```
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        function getAgeFromBirth() {
            var y = new Date().getFullYear();
            return y - this.birth;
        }
        return getAgeFromBirth();
    }
};
xiaoming.age(); // Uncaught TypeError: Cannot read property 'birth' of undefined
```

#### 函数方法：apply
`apply`是函数本身的方法，可以控制函数中`this`指向哪个对象。
`apply()`接收两个参数,第一个参数就是需要绑定的`this`变量，第二个参数是Array，表示函数本身的参数。
```
function getAge(){
	var y = new Date().getFulYear();
	return y - this,birth;
}

var xiaoming = {
	name:'小明',
	birth:1990,
	age:getAge
};
xiaoming.age();//25
getAge.apply(xiaoming,[]);//25，this指向xiaoming，参数为空
```

#### 函数方法：call
唯一与`apply`区别是：
	* `apply()`把参数打包成`Array`再传入；
	* `call()`把参数按顺序传入。

```
Math.max.apply(null,[3,4,5]);//5
Math.max.call(null,3,4,5);//5
```
对普通函数调用，通常把`this`绑定为null。

#### 装饰器
利用`apply()`，可以动态改变函数的行为。

* 解决问题：假设想统计`parseInt()`调用了多少次：
```
var count = 0;
var oldParseInt = parseInt();//保存原函数
window.parseInt = function(){//自定义方法替换原函数
	count += 1;
	return oldParseInt.apply(null,agments);//调用原函数
};
```

### 高阶函数
一个函数接收另一个函数作为参数，这种函数就称之为**高阶函数**。
```
function add(x,y,f){
	return f(x) + f(y);
}
//调用
add(-5,6,Math.abs);// f(x) + f(y) ==> Math.abs(-5) + Math.abs(6) 返回11
```

#### `map()`方法
`map()`方法定义在`Array`中，调用`Array`的`map()`方法，传入自定义的函数，就得到了一个新的`Array`作为结果：
```
function pow(x){
	return x*x;
}
var arr = [1,2,3,4,5,6,7,8,9]
var results = arr.map(pow(x));//得到结果 [1, 4, 9, 16, 25, 36, 49, 64, 81]
```

***注意：map()传入的参数是函数对象本身。***


#### `reduce()`方法
Array的`reduce()`方法把一个函数作用在这个Array的每个元素`[x1,x2,x3,...]`上，这个自定义函数必须接收两个参数，`reduce()`会把
前一个元素的计算结果继续和下一个元素做累积计算。（递归计算）
```
[x1,x2,x3,x4].reduce(f) = f(f(f(x1,x2),x3),x4)
```
例子：对一个Array求和：
```
var arr = [1,3,5,7,9];
var result = arr.reduce(function (x,y){
	return x + y;
});// 25
```

#### `filter()`方法
Array的`filter()`方法接收一个函数，该函数作用域每个元素，然后根据返回值决定是否丢弃该元素。
```
var arr = [1,2,3,4,5,6,9,10,15];
var r = arr.filter(function(x){
	return x % 2!== 0;
});
r;// [1, 5, 9, 15]，只保留奇数
```
* filter()可以接收三个参数，分别是`元素本身`，`元素位置`和`数组本身`。
```
var arr = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
r = arr.filter(function(element,index,sef){
	return self.indexOf(element) === index;
}); // 巧妙去重,indexOf()只会返回数组第一个元素，删除其他非第一个元素的下标
```

#### `sort()`方法
Array的`sort()`方法是用于排序的，可以直接使用默认的排序规则，但结果很蛋疼。
```
[10, 20, 1, 2].sort(); // [1, 10, 2, 20]
```
* `sort()`方法的默认排序规则是：字符串根据ASCI码进行排序；先默认把所有元素先转换为Strign再排序。

* `sort()`方法会直接对Array进行修改，它返回的结果仍是当前Array；

* `sort()`是高阶函数，也可以接收一个自定义函数进行排序。

通常规定，对于两个元素x和y，如果认为x < y，则返回-1，如果认为x == y，则返回0，如果认为x > y，则返回1，这样，排序算法就不用关心具体的比较过程，而是根据比较结果直接排序。
```
var arr = [10, 20, 1, 2];
arr.sort(function (x, y) {//接收两个参数，返回-1,0,1
    if (x < y) {
        return -1;
    }
    if (x > y) {
        return 1;
    }
    return 0;
});
console.log(arr); // [1, 2, 10, 20]
```

#### `every()`方法
`every()`方法可以判断数组的所有元素是否满足测试条件。
```
var arr = ['Apple', 'pear', 'orange'];
arr.every(function(s){
	return s.length > 0;
});
// 返回 true, 因为每个元素都满足s.length>0
```

#### `find()`方法
`find()`方法用于查找数组中第一个符合条件的元素，如果找到了则返回这个元素，否则返回`udnefined`
```
var arr = ['Apple', 'pear', 'orange'];
var str = arr.find(function(s){
	return s.toLowerCase() === s;
});
str; //pear 因为pear全部都是小写
```

#### `findIndex()`方法
`findIndex()`与find()方法类似，也是查找符合条件的第一个元素，不同在于`findIndex()`返回元素的索引，若没找到返回-1.
```
var arr = ['Apple', 'pear', 'orange'];
arr.findIndex(function(s){
	return s.toLowerCase() === s;
});
//返回1，因为pear索引是1
```

#### `forEach`方法
`forEach()`方法常用于遍历数组，传入的函数不需要返回值，且不会返回新的数组。
```
var arr = ['Apple', 'pear', 'orange'];
arr.forEach(console.log); // 依次打印每个元素
```

### 闭包
闭包就是携带状态的函数，并且它的状态可以完全对外隐藏起来。

#### 函数作为返回值
```
//该函数将另一个函数作为返回值
function lazy_sum(arr){
	return function(){
		arr.reduce(function(x,y){
			return x + y;
		})
	};
}
var f = lazy_sum([1, 2, 3, 4, 5]);
f();//在调用f时，才真正计算结果
```

* 当调用lazy_sum()时，每次都返回一个新的函数，即使传入相同的参数，两个返回的结果也互不影响。
```
var f1 = lazy_sum([1, 2, 3, 4, 5]);
var f2 = lazy_sum([1, 2, 3, 4, 5]);
f1 === f2; // false
```

* 返回闭包时要牢记：返回函数不要引用任何循环变量，或者后续会发生变化的变量。
如果要引用循环变量，则在创建一个函数，将该函数的参数绑定到循环变量当前值，这样再循环变量发生变化，传入
该函数的参数也不会发生变化。
```
function count(){
	var arr = [];
	for(var i = 1; i <= 3;i++){
		arr.push(function(i){
			return i * i;
		});
	}
}
```
修改后：
```
function count(){
	var arr = [];
	for(var i=1;i<=3;i++){
		arr.push((function(n){
			return function(){
				return n*n;
			}
		})(i));
	}
}
```

* 创建一个匿名函数并立刻执行的语法：
```
(function(x){
	return x * x;
})(3);// 9 
```
***注意：如果不将函数用`()`括起来，由于JavaScript语法解析问题，会报SyntaxError错误。***

* 利用闭包实现一个私有变量：
```
function create_counter(initial){
	var x = initial || 0;
	return { //返回一个属性是闭包的对象
		inc:function(){
			return x += 1;
		}
	}
}
var c1 = create_counter();
c1.inc();//1
c1.inc();//2
var c2 = create_counter(10);
c2.inc(); // 11
```
在返回的对象中，实现了一个闭包，该闭包携带了局部变量x，并且，从外部代码根本无法访问到变量x。
换句话说，闭包就是携带状态的函数，并且它的状态可以完全对外隐藏起来。

#### 箭头函数
ES6标准新增了一种新的函数：Arrow Function（箭头函数）。
箭头函数相当于匿名函数，并且简化了函数定义。
```
x => x*x	相当于	function(x){ return x * x; }	
```

* 如果箭头函数只有一条语句，可以省略`{...}`和`return`,如果如果包含多条语句，就不能省略了。
* 如果参数不是一个，就需要用`()`括起来。
```
(x,y) => {
    if (x > 0) {
        return x * y;
    }
    else {
        return - x * y;
    }
}
```

* 如果返回一个单表达式对象，需要注意与函数体`{...}`的冲突。
```
x => { name:'小明' } //SyntexErryr错误，因为生命对象的{}与函数体{}冲突了。
//正确写法:
x => ({ name:'小明' })
```

#### 箭头函数内的this
箭头函数内部的this是词法作用域，由上下文确定。
```
var obj = {
	birth:1990,
	getAge : function(){
		var fn = function(){
			return new Date().getFulYear() - this.birth; //嵌套函数中的this指向window或undefined
		}
		return fn();
	}
};
```
箭头函数完全修复了this的指向：
```
var obj = {
	birth: 1990,
	getAte:function(){
		var fn = ()=> new Date().getFullYear() - this.birth;//this指向obj对象
		return fn;
	}
};
```

* 由于`this`在箭头函数中已经按词法作用域绑定了，所以，`call()`和`apply()`方法调用箭头函数时，无法对this进行绑定。（第一个参数被忽略）

### generator（生成器）
generator(生成器)shi ES6标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次。

* generator定义：
generator使用`function*`定义，并且除了return语句，还可以使用`yield`返回多次。
```
function* foo(x){
	yield x + 1;
	yield x + 2;
	return x + 3;
}
```
如编写一个返回斐波那契数列的生成器：
```
function* fib(max){
	var a = 0,b = 1,n = 0;
	while(n < max){
		yield a;
		[a,b] = [b,a+b];
		n++;
	}
	return;
}
filb();// fib {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window} 与调用函数不一样，filb()只是创建了一个generator对象。
```
调用生成器有两个方法：
1. 使用generator的`nex()`方法
```
var f = filb(2);
f.next();//{value: 0, done: false}
f.next();//{value: 1, done: false}
f.next(); // {value: undefined, done: true}
```
`next()`方法会执行generator代码，每次遇到`yield x;`就返回一个对象`{value:x,down:true/false}`,然后'暂停'。
`value`就是`yield`的返回值。
`done`表示这个generator是否已经执行结束了，如果为true，则`value`就是`return`的返回值。（猜测：generator碰到return就执行结束了。）

2. 使用`for ... of`循环迭代generator对象，这种方式不需要自己判断`done`。
```
for(var x of fib(2)){
	console.log(x);
}
//打印 0,1
```

* generator还可以把异步回调变成“同步”代码
```
ajax('http://url-1', data1, function (err, result) {
    if (err) {
        return handle(err);
    }
    ajax('http://url-2', data2, function (err, result) {
        if (err) {
            return handle(err);
        }
        ajax('http://url-3', data3, function (err, result) {
            if (err) {
                return handle(err);
            }
            return success(result);
        });
    });
});
```
使用generator：看上去是同步的代码，实际执行是异步的。
```
try {
    r1 = yield ajax('http://url-1', data1);
    r2 = yield ajax('http://url-2', data2);
    r3 = yield ajax('http://url-3', data3);
    success(r3);
}
catch (err) {
    handle(err);
}
```


#####练习：
1. 利用reduce()求积：
return arr.reduce(function(x,y){});

2. 字符串转Number：思路，先将String拆分成字符串数组，数组再使用map()方法转为数字数组，最后使用reduce()方法计算累加。
var arr = [];
for(let i = 0;i<s.length;i++){
     arr.push(s[i]);
}
var arr2 = arr.map(function(str){
    return str - 0;
});
var num = arr2.reduce(function(x,y){
	return x * 10 + y;
})
console.log(arr2);
return num ;

3. 规范命名：
return arr.map(function(name){
	return name.substring(0,1).toUpperCase() + name.substring(1,name.length).toLowerCase();
});


4. 修改小明错误：
问题核心在parseInt()函数上，该函数即可以传入一个参数，也可以传入两个参数(string,radix)。
第一个参数代表被解析的值，第二个参数是声明底数(被转换的"数字"是多少进制的)。
修改代码，为map()方法中内嵌一个函数，将参数都打印出来：
结果是：x = 1 y = 0 z = 1,2,3 额外参数:
可以看到map()默认传入了三个参数，参数1：数组中元素；参数2：数组元素下标；参数3：Array本身
小明直接使用arr.map(parseInt),默认为parseInt传入了三个值，所以用到了parseInt两个参数的方法。

有关parseInt的radix，当遇到0、undefined或未被指定时，parseInt有如下行为：
1）被转换的字符串起于"0x"/"0X" --> 十六进制转为十进制；
2）被转换的字符串起于"0" --> 八进制或十进制（由解释器决定）转为十进制；
3）被转换字符串起于其他值 --> 十进制转为十进制。

当arr = [1,2,3]时，arr.map(parseInt)实际为：
parseInt('1', 0);    // 按十进制转换'1'
parseInt('2', 1);    // 按一进制转换'2'，但一进制中只有0没有1
parseInt('3', 2);    // 按二进制转换3，但二进制中只有0和1没有2

答案：
r = arr.map(function(x,y,z,...rest){ 
    console.log('x = ' + x + ' y = ' + y + ' z = ' + z + ' 额外参数:' + rest);// 打印x = 1 y = 0 z = 1,2,3 额外参数:
    return parseInt(x) 
});








































