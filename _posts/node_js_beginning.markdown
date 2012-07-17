Title: nodejs 初学记录
Author: Dazuo Sun
Date: Fri April 1 2012 10:39:00 GMT+0800 (China Standard Time)
Lang: nodejs
###1.首先是安装
参考[这里](http://www.infoq.com/cn/articles/nodejs-npm-install-config)
由于nodejs不支持原生态的windows，在windows上安装稍显费力。



###2.了解nodejs

请看nodejs 创始人Ryan Dalh视频[这里](http://www.youtube.com/watch?v=jo_B4LTHi3I)


这是一个不懂什么是nodejs的人必看的视频。
Ryan 用一个简单的web server 演示了nodejs的一个helloworld程序，并反复地证明nodejs的non-blocking特性带来的效率优势。
最后Ryan说了几个nodejs目前存在的问题：
1.由于是新兴技术，基础组件并不是十分完善。例如数据库链接那一块。当然这不是十分重要的问题。
2.不能像java一样在出错时打出堆栈信息，给排查问题带来很大麻烦。这是因为nodejs non-blocking特性带来的负面效果，因为nodejs他是有可能不是按照代码顺序执行的（当某行代码开销大的时候，他就直接跳到下一行执行）。

###3.入门书籍
请看[这里](http://www.nodebeginner.org)

顺便附上一个js菜鸟的笔记：

nodejs学习笔记

一、先是恶补了三点javascript的基本知识

    1.callback，即执行完之后调用的函数
	
    2.javascript对象的本质：In JavaScript,? objects are just collections of name/value pairs - think
    of a JavaScript object as a dictionary with string keys.
	
    3.javascript是对象，而他的方法呢？其实他的方法通过value体现，因为js中的fuction也是一个value嘛

二、关于nodejs的包机制，require和export都非常简单，跟python一样

三、nodejs是最引人注目的噱头是non-blocking。对于non-blocking，我有这种疑惑，如果下面一行代码依赖到上面一行代码的执行结果，而上面一行代码开销很大，</span>non-blocking之后没执行完上一行代码直接跳到下一行代码执行会不会有问题？

比如：

    var a = doExpensiveThing();

    a.doOtherThing();

第一句话没执行完而去执行第二句话明显是有问题的，对于这种问题，nodejs需要程序员自己判断某一行代码执行的开销，如果开销大，就把必须依赖这行代码结果的其他代码挪到callback里面，强制在被依赖的代码执行完之后执行。通过这种方式解决上面这个问题，相当于把代码执行顺序交给程序员自己控制。我不懂的一点是：如此依赖nodejs是一个非线性执行的代码，一行代码的执行开销在不同的环境下都不一样，把代码的执行顺序权交给程序员，虽然提高了灵活性，但未免太灵活了，程序员能控制的来吗？在不同的环境下会不会有截然不同的处理方式?

不知道这种理解有没有问题？
