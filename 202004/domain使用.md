## domain实现跨域

> 因项目需要，需要跨域，而且是在同一个基础域名下，就选择domain来实现，过程较为简单。

### 前提条件
> 需跨域的两个域名必须属于同一个基础域名，而且所用的协议(http或https)，端口号必须要一致。否则无法利用document.domain进行跨域。  
> > 1. JavaScript出于对安全性的考虑，而禁止两个或者多个不同域名的页面进行相互操作。
> > 2. 相同的页面在相互操作的时候，是不会任何有问题的。

### iframe之间的操作
> 例如：
> > aaa.com的一个网页中（a.html），利用iframe引入来一个bbb.com里的页面（b.html）  
> > 这时候在a.html中可以看到b.html的内容，但是却不能利用javascript来操作它。因为这两个页面属于不同的域，在操作之前，js会检测两个页面的域是否相等，如果相等，就允许操作，如果不相等，就会拒绝操作。  
> > 这里不可能把a.html与b.html利用JavaScript改成同一个域。因为它们的基础域名不相等。（强制用JavaScript将它们改成相等的域的话，会报“参数无效错误。”）  
> 
> 另外一种情况：
> > 如果两个子域名：aaa.xxx.com和bbb.xxx.com；aaa里的页面（a.html）引入里bbb里的一个网页（b.html），这时a.html里同样不能操作b.html里面的内容。因为document.domain不一样，一个是aaa.xxx.com，另外一个是bbb.xxx.com。
> 
> 这时我们就可以通过JavaScript，将两个页面的domain改成一样的。
> > 只需要在a.html里与b.html里都加入
> > ```js
> >  document.domain = 'xxx.com';
> > ```
> 这样两个页面就可以相互操作了。也就实现了同一基础域名之间的“跨域”；

### cookie的domain
> cookie虽然是由一个网页所创建，但并不只是创建cookie的网页才能读取该cookie。  
> 在默认情况下，与创建cookie的网页在同一个目录或者子目录下的所有网页都可以读取该cookie。但是如果在这个目录下还有子目录，要使在子目录中也可以访问。则需要使用path参数设置cookie。
> ```js
>   // test目录可以访问
>   document.cookie = "name=" + escape("zhangsan") + "; path=/test"
>   // 整个域名下都可以访问
>   document.cookie = "name=" + escape("zhangsan") + "; path=/"
> ```

> 当如果在bbb.xxx.com域名下访问aaa.xxx.com里的cookie，就需要是用domain参数了。  
> 例如，在aaa.xxx.com里设置cookie的domain，在bbb.xxx.com里就可以访问到了。
> ```js
>   // 注意：domian基础域名参数前面最好带一个.
>   document.cookie = "name=" + escape("zhangsan") + "; path=/; domain=.xxx.com"
> ```

### 参考文档
> 1. [js设置document.domain实现跨域的注意点分析](https://www.jb51.net/article/66497.htm)
> 2. [JavaScript中cookie的路径(path)和域(domain)](https://www.cnblogs.com/ricky_li/p/3365064.html)
