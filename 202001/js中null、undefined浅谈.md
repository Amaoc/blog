# js中null、undefined浅谈
大多数计算机语言，有且只有一个表示“无”的值，比如，C语言的NULL，Java语言的null，Python语言的None，Ruby语言的nil。
*  为啥JavaScript语言居然有两个表示“无”的值：undefined和null  *

### 历史原因
1995年JavaScript诞生时，最初像Java一样，只设置了null作为表示“无”的值。  
根据C语言的传统，null被设计成可以自动转为0。

但是Brendan Eich觉得这样做还不够，有两个原因：
1. null像在Java里一样，被当成一个对象。但是，JavaScript的数据类型分成原始类型（primitive）和合成类型（complex）两大类，Brendan Eich觉得表示“无”的值最好不是对象。

2. JavaScript的最初版本没有包括错误处理机制，发生数据类型不匹配时，往往时自动转换类型或者默默地失败。Brendan Eich觉得，如果null自动转为0，很不容易发现错误。

因此，Brendan Eich又设计了一个undefined。

### 最初设计
JavaScript的最初版本时这样区分的：
1. null 是一个表示“无”的对象，转为数值时为0；
2. undefined 是一个表示“无”的原始值，转为数值是为NAN；
``` bash
Number(null)
# 0

5 + null
# 5

Number(undefined)
# NAN

5 + undefined
# NAN
```

### 目前的用法
按照最初的设计区分，在实践中很快就被证明不可行。实践中有很多需要注意的地方。
1. null
null 是基本数据类型之一，值仅有一个，即为null。表示“空对象”（因此类型检测返回对象），即如果有对象就会是一个具体的对象，如果没有对象，就是null。  
典型用法：
    1. 作为函数的参数，表示该函数的参数不是对象；
    2. 作为对象的原型链的终点。
    ``` bash
    Object.getPrototypeOf(Object.prototype)  // null
    typeof null      // Object
    ```
    如果定义一个变量准备在将来用来保存对象，那么最好将该变量初始化为null而不是其他值。

2. undefined
undefined 是基本数据类型之一，值仅有一个，即为undefined。表示“缺少值”（因此类型检测返回 undefined），即此处应该有一个值，但是还没有定义。  
典型的用法：
    1. 变量被声明来，但没有赋值是，就等于 undefined 。
    2. 调用函数时，应该提供的参数没有提供，该参数就是undefined。
    3. 对象没有赋值的属性，该属性的值为 undefined。
    4. 函数没有返回值，默认返回 undefined。
    

### 参考文档
1. [null 和 undefined 的区别](https://www.cnblogs.com/haishen/p/10718715.html)
2. [null 和 undefined](https://cloud.tencent.com/developer/article/1534974)
3. [null 和 undefined 的区别](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)
