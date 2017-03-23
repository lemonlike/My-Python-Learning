- 响应式布局声明  
```
<meta name="viewport" content="width=device-width, initial-scale=1">
```
- bootstrap.css和bootstrap.min.css的区别
bootstrap.css 和 boostrap.min.css 的区别就是：前者是未压缩的，后者是压缩过的。
一般情况下，未压缩的用于开发环境，如果程序出错方便调试。而压缩过的用生生产环境，把bootstrap.css中的空格和不必要的注释全部去掉了，大大减少网络数据传输量，便之更快更节约流量。通过工具压缩，令相同的代码所占空间更小，从而提升web性能，减少宽带的压力。

- 中文文档  
[http://v3.bootcss.com/](http://v3.bootcss.com/)
- 英文文档  
[http://getbootstrap.com/](http://getbootstrap.com/)

- role 属性在 html 中的作用
html 里面的 role 本质上是增强语义性，当现有的HTML标签不能充分表达语义性的时候，就可以借助 role 来说明。通常这种情况出现在一些自定义的组件上，这样可增强组件的可访问性、可用性和可交互性。
role 的作用是描述一个非标准的tag的实际作用。比如用 div 做 button，那么设置 div 的 role=“button”，辅助工具就可以认出这实际上是个 button。

- 要想让图片充满整个父级容器，就设置图片宽度和高度均为100%