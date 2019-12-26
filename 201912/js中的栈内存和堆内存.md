# js中的栈内存和堆内存
JavaScript的内存空间分为栈(stack)、堆(heap)、池(或叫栈中);

### 栈内存和堆内存简介
1. 栈数据结构
JavaScript中并没有严格意义上区分栈内存和堆内存。  
执行上下文的执行顺序借用了栈数据结构的存取方式；
栈空间的特点：先进后出，后进先出；  
![栈数据结构](./images/1.webp, '栈数据结构')  
由于栈具有后入先出的特点，所以任何不在栈顶的元素都无法访问。  
为了得到栈底的元素，必须先拿掉上面的元素；  
类似乒乓球盒子来分析栈的存取方式。  
  
栈会自动分配内存空间，物理内存是连续的，可以存放基本类型（Boole,Number,String,undefined,null,Symbol），简单的数据段，引用类型的物理地址；
占用空间小（大小固定），通过按值来访问，属于被频繁使用的数据。  
PS：闭包中的基本数据类型变量不会保存在栈内存中，而是保存在堆内存中。




## 参考文案
1. [浅析js中的栈内存和堆内存](https://www.cnblogs.com/heioray/p/9487093.html)
2. [中高级前端必须了解的--JS中的栈内存和堆内存](https://blog.csdn.net/a59612/article/details/93661354)
3. [JavaScript栈内存与堆内存](https://www.jianshu.com/p/0b18e120955b)
4. [详解JavaScript栈内存与堆内存](https://www.jb51.net/article/159120.htm)
5. [js中的栈内存和堆内存](https://blog.csdn.net/qq_36747861/article/details/84958366)
