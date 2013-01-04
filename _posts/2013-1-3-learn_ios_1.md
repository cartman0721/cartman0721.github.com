###学习资料

* stanford university的视频资料 [点我](http://i.youku.com/u/UOTYxNjIxNTY=/videos)

	共有十七八课的样子，有中文字幕

* 官方的Getting started  [点我](https://developer.apple.com/library/ios/#referencelibrary/GettingStarted/RoadMapiOS/chapters/Introduction.html)
	
	个人 觉得对于入门学习的人来说，看视频比看文档效率更高一些，因为有时候文档上婆婆妈妈的一大堆文字，只消视频上几个动作就能将清楚了。

###objective-c语法与java的比较

1.方法访问权限：
 定义在.h文件中的等同于public方法  定义在.m文件中的是private方法
 
2.@synthesize关键字


	@synthesize operandStack =_operandStack;
	
可以自动生成属性的getter和setter方法，上面这段代码相当于加了以下这段代码

	- (NSMutableArray *)operandStack{
   	 	return _operandStack;
	}
	- (void)setOperandStack:(NSMutableArray *)newOperandStack{
    	_operandStack = newOperandStack;
	}
		

另外变量_operandStack未在代码里申明，编译器会自动声明_operandStack，所以不会报错。
用self.operandStack相当于调用了setter或者getter方法，而用_operandStack相当于直接访问变量  _operandStack

	self.operandStack = [[NSMutableArray alloc] init];
	//这里的self.operandStack 相当于调用了setter方法，即上面代码等同于
	[self setOperandStack:[[NSMutableArray alloc] init]]
	
	[self.operandStack addObject:operation];
	//这里的self.operandStack 相当于调用了getter方法，即上面代码等同于
	[[self operandStack] addObject:operation]


3.基本类型和包装类型

Objective-C中的基本类型和C语言中的基本类型一样.主要有:int,long,float,double,char,void, bool等.
在Foundation中,也为些数据定义了别名,如:NSInteger为long,CGFloat为double,BOOL等.
基本类型的变量存放的实际的值，封装类型的变量存放的是变量的地址，通常以指针的形式表示，如NSString不是一个基本类型。

	NSNumber *foo = XXXX;
	NSInteger foo =XXXX;

4.方法定义

*  -表示成员方法；+表示类方法。
*  多参数的方法定义和调用：

	Objective-c 多参数方法的定义和调用方式比较诡异，每一个参数前面都有一个唯一表示，他们共同组成了这个方法的签名，如：
	
		-(void) setTo: (int) n over: (int) d //方法定义 setTo 和over共同组成了方法的唯一签名
		 [instanceXXX setTo: 100 over: 200];//方法调用
		 
	据说这么做的原因是为了代码的可读性，所以objective-c的方法定义都很长，幸亏有xcode的方法自动补全功能，否则ios程序员就变成了打字员。
	
5.@selector
类似C语言中的函数指针，SEL是一个函数指针类型，可以通过performSelector执行.

	@implementation ClassForSelectors
	- (void) fooNoInputs {
	NSLog(@"Does nothing");
	}
	- (void) fooOneIput:(NSString*) first {
	NSLog(@"Logs %@", first);
	}
	- (void) fooFirstInput:(NSString*) first secondInput:(NSString*) second {
	NSLog(@"Logs %@ then %@", first, second);
	}
	 
	- (NSArray *)abcWithAAA: (NSNumber *)number {
	int primaryKey = [number intValue];
	NSLog("%i", primaryKey);
	}
	 
	- (void) performMethodsViaSelectors {
	[self performSelector:@selector(fooNoInputs)];
	[self performSelector:@selector(fooOneInput:) withObject:@"first"];
	[self performSelector:@selector(fooFirstInput:secondInput:) withObject:@"first"withObject:@"second"];
	}
	 
	- (void) performDynamicMethodsViaSelectors {
	MethodForSelectors * mfs = [MethodForSelectors alloc];
	NSArray *Arrays = [NSArray arrayWithObjects:@"AAA", @"BBB", nil];
	for ( NSString *array in Arrays ){
	SEL customSelector =NSSelectorFromString([NSStringstringWithFormat:@"abcWith%@:", array]);
	mfs = [[MethodForSelectors alloc] performSelector:customSelector withObject:0];
	}
	}
	@end
	

从这一点看objective-c还是一门比较灵活的语言，performDynamicMethodsViaSelectors做的事情类似java里的通过反射机制调用，不同的是java中如果对象中不存在此方法会抛异常，而objective-c会什么事情都不做。

###遇到的问题

新手上路，难免遇到一些因为对IDE不熟造成的环境问题，大部分都忘记了

1.问题：compilation warning: no rule to process file for architecture i386
  原因：没有把.h文件加入编译，解决方法和问题分析见[这里](http://stackoverflow.com/questions/6509600/compilation-warning-no-rule-to-process-file-for-architecture-i386)

2.问题：mac USB口一插入iphone xcode就崩溃，还没找到原因，不知为何，还望高手解答。
