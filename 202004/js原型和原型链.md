## js的原型和原型链

### 普通函数和函数对象
> JavaScript中，万物皆对象！但是对象也是有区别的。分为普通函数和函数对象，Object、Function是JS中自带的函数对象。
> ```js
> var o1 = {};
> var o2 = new Object();
> var o3 = new f1();
> 
> function f1() {};
> var f2 = function() {};
> var f3 = new Function('str', 'console.log(str)');
> 
> console.log(typeof Object); // function
> console.log(typeof Function); // function
>
> console.log(typeof f1); // function
> console.log(typeof f2); // function
> console.log(typeof f3); // function
> 
> console.log(typeof o1); // object
> console.log(typeof o2); // object
> console.log(typeof o3); // object
> ```
> 在上面的例子中，o1、o2、o3为普通的对象，f1、f2、f3为函数对象。  
> 怎么区分？其实很简单：  
> 凡是通过new Function() 创建的对象都是函数对象，其他的都是普通对象。f1、f2归根结底都是通过new Function() 的方式进行创建的。Function Object也都是通过new Function() 创建的。

### 构造函数
> 我们先复习一下构造函数的知识：
> 
> ```js
> function Person(name, age, job) {
>   this.name = name;
>   this.age = age;
>   this.job = job;
>   this.sayName = function() {
>     console.log(this.name)
>   }
> }
> var person1 = new Person('zhangsan', 28, 'Software Engineer');
> var person2 = new Person('lisi', 23, 'Doctor');
> ```
> 
> 上面的例子中的person1和person2都是Person的实例。这两个实例都有一个constructor（构造函数）的属性，该属性(是一个指针)指向Person。即：
> 
> ```js
> console.log(person1.constructor === Person); // true
> console.log(person2.constructor === Person); // true
> ```
> 
> 我们要记住两个概念（构造函数，实例）：  
> person1和person2都是构造函数Person的实例。  
> 一个公式：  
> 实例的构造函数属性（constructor）指向构造函数。

### 原型对象
> 在JavaScript中，每当定义一个对象（函数也是对象）的时候，对象中都会包含一些预定义的属性。其中每个函数对象都有一个prototype属性，这个属性指向函数的原型对象。
> 
> ```js
> function Person() {};
> Person.prototype.name = 'zhangsan';
> Person.prototype.age = 28;
> Person.prototype.job = 'Softwar Engineer';
> Person.prototype.sayName = function() {
>   console.log(this.name);
> }
> var person1 = new Person();
> person1.sayName(); // 'zhangsan';
> 
> var person2 = new Person();
> person2.sayName(); // 'zhangsan';
> 
> console.log(person1.sayName === person2.sayName); // true; 
> ```
> 
> 我们得到了文本第一【定律】：
> ```bash
> 每个对象都有__proto__属性，但只有函数对象才有prototype属性。
> ```
>   
> 那什么是原型对象呢？  
> 我们把上面的例子改一改就会明白了：
> ```js
> Person.prototype = {
>   name: 'zhangsan',
>   age: 28,
>   job: 'Software',
>   sayName: function() {
>     console.log(this.name);
>   }
> }
> ```
> 原型对象，顾名思义，它就是一个普通对象。  
> 在上面我们给A添加了四个属性：name，age，job，sayName。其实它还有一个默认属性：constructor。
> > 在默认情况下，所有的原型对象都会自动获得一个constructor（构造函数）的属性，这个属性（是一个指针）指向prototype属性所在的函数（Person）。  
> > 即 Person.prototype.constructor === Person;
> 











### 参考文档
> 1. [最详尽的 JS 原型与原型链终极详解，没有「可能是」。（一）](https://www.jianshu.com/p/dee9f8b14771)
> 2. [最详尽的 JS 原型与原型链终极详解，没有「可能是」。（二）](https://www.jianshu.com/p/652991a67186)
> 3. [最详尽的 JS 原型与原型链终极详解，没有「可能是」。（三）](https://www.jianshu.com/p/a4e1e7b6f4f8)
> 