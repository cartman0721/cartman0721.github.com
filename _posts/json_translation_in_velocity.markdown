Title: 悲剧启示录 1------velocity中json转译的问题
Author: Dazuo Sun
Date: Mon April 9 2011 06:23:00 GMT+0800 (China Standard Time)
Lang: js
   
   今天转义json的特殊字符，一路上磕磕绊绊，几次柳暗花明又一村的感觉，整个过程还是蛮有意思的。

###问题：

众所周知，Json是个很脆弱的玩意儿，在json中插入一些特殊字符，如 n r等，就会破坏json的整体结构，导致json根本无法被识别。

比如下面这段：

    {
   
    "code":'$!ajaxResult.code',
   
    "message":'$!ajaxResult.message',
   
    "datas":'$!ajaxResult.datas'
    }

假设ajaxResult. datas里存了一个n字符，这段json就会被破坏导致根本无法被识别。

解决这个问题是个很有意思的过事情，经历了一下几个过程

###1.土鳖方案：
String的replaceAll方法：直接在velocity中写$!ajaxResult.datas.replaceAll(“n”,””).replaceAll(“r”,””)。将那些祸害大局的特殊字符通通替换为空。

###2.用javaScriptUtils

因为Json里的特殊字符并非只有n r，偶尔插入的一个””导致整个json请求的失败，而且强制将这些字符格杀勿论也并不合理，万一业务方就想换下行呢（这个有点钻牛角尖了），

于是用了org.springframework.web.util.JavaScriptUtils.javaScriptEscape(String)，将特殊字符前面都加了强行转译。

代码如下：

       StringBuffer filtered = new StringBuffer(input.length());

       char prevChar = 'u0000';

       char c;

       for (int i = 0; i < input.length(); i++) {

           c = input.charAt(i);

           if (c == '"') {

              filtered.append(""");

           }

           else if (c == ''') {

              filtered.append("'");

           }

           else if (c == '') {

              filtered.append("\");

           }

           else if (c == '/') {

              filtered.append("/");

           }

           else if (c == 't') {

              filtered.append("t");

           }

           else if (c == 'n') {

              if (prevChar != 'r') {

                  filtered.append("n");

              }

           }

           else if (c == 'r') {

              filtered.append("n");

           }

           else if (c == 'f') {

              filtered.append("f");

           }

           else {

              filtered.append(c);

           }

           prevChar = c;

 

       }

       return filtered.toString();

}

###3.封装javaScriptUtils

但是修改完之后依然有问题，当字符里包含字符 ” 或 ’ 的时候依然会导致真个请求的失败。velocity本身出于防范js攻击的安全性考虑，会将 字符” 和 ’转译成'和 &quot。所以当输入一个”之后，他会经过这么一个过程 "------->/"------->/&#39,导致最终虽然消除了引号，但是多出的这个 “/”不能以转译符的身份存在。

最终修改的结果是：包装了javaScriptEscape类，去除了对双引号和单引号的转译，因为velocity会对其自动转译。即

      StringBuffer filtered = new StringBuffer(input.length());

       char prevChar = 'u0000';

       char c;

       for (int i = 0; i < input.length(); i++) {

           c = input.charAt(i);

          

           else if (c == '') {

              filtered.append("\");

           }

           else if (c == '/') {

              filtered.append("/");

           }

           else if (c == 't') {

              filtered.append("t");

           }

           else if (c == 'n') {

              if (prevChar != 'r') {

                  filtered.append("n");

              }

           }

           else if (c == 'r') {

              filtered.append("n");

           }

           else if (c == 'f') {

              filtered.append("f");

           }

           else {

              filtered.append(c);

           }

           prevChar = c;

 

       }

       return filtered.toString();

}

Ok，大功告成！

###后记：
在第三步的时候脑子比较混乱，一根筋地认为在这样的表达式JavaScriptUtils.javaScriptEscape ($!ajaxResult.message)中，如果ajaxResult.message里存在 ” ,velocity会把” 转译成&#39传给javaScriptEscape方法，其实这是错的。Velocity只会在页面渲染的时候进行转译，事后看看这是一个多么简单多么不言而喻的事情，但在思考的时候往往就会陷入这个坑而不可自拔。因为这点认识的误区我还尝试过如何在webx配置中把velocity中的自动转译功能给去掉，但这样会导致另外一个问题，用户在输入类似下面的html标签时就会悲剧
      
      <input/>
      
如此就会让自己纠结于一个看起来很棘手但实际并不存在的问题。。绕了个大圈。。想问题时保持头脑清晰很重要！

 