Title: regex 学习记录
Author: Dazuo Sun
Date: Tue May 22 2012 11:13:00 GMT+0800 (China Standard Time)
Lang: regex

看到一篇质量颇高的关于正则表达式的文章（[点我](http://deerchao.net/tutorials/regex/regex.htm))，清楚明白，循序渐进，打消我了一度对正则表达式的畏惧感，至少不用一写正则表达式就要打开google了。


#1.常用的元字符
<table cellspacing="0">

<thead>

<tr>

<th scope="col">代码</th>



<th scope="col">说明</th>

</tr>

</thead>

<tbody>

<tr>

<td><span class="code">.</span></td>

<td><span class="desc">匹配除换行符以外的任意字符</span></td>



</tr>

<tr>

<td><span class="code">\w</span></td>

<td><span class="desc">匹配字母或数字或下划线或汉字</span></td>

</tr>

<tr>

<td><span class="code">\s</span></td>



<td><span class="desc">匹配任意的空白符</span></td>

</tr>

<tr>

<td><span class="code">\d</span></td>

<td><span class="desc">匹配数字</span></td>

</tr>

<tr>



<td><span class="code">\b</span></td>

<td><span class="desc">匹配单词的开始或结束</span></td>

</tr>

<tr>

<td><span class="code">^</span></td>

<td><span class="desc">匹配字符串的开始</span></td>

</tr>



<tr>

<td><span class="code">$</span></td>

<td><span class="desc">匹配字符串的结束</span></td>

</tr>

</tbody>

</table>
###注意点：

    1.\b用来匹配全字符 如表达式\bhi\b 可以匹配字符串“hi 123”，却不能匹配“hi123”
    2.如果表达式开始没有加^,结尾没有加$,则当字符串含有正则表达式的内容就匹配成功，否则必须字符串整个匹配才能成功，比如用表达式“hi”能匹配“hi123”，而“^hi$”就不能。这一点自己以前常常写错。

#2.常用的限定符
<table cellspacing="0">


<thead>

<tr>

<th scope="col">代码/语法</th>

<th scope="col">说明</th>

</tr>



</thead>

<tbody>

<tr>

<td><span class="code">*</span></td>

<td><span class="desc">重复零次或更多次</span></td>

</tr>

<tr>

<td><span class="code">+</span></td>



<td><span class="desc">重复一次或更多次</span></td>

</tr>

<tr>

<td><span class="code">?</span></td>

<td><span class="desc">重复零次或一次</span></td>

</tr>

<tr>



<td><span class="code">{n}</span></td>

<td><span class="desc">重复n次</span></td>

</tr>

<tr>

<td><span class="code">{n,}</span></td>

<td><span class="desc">重复n次或更多次</span></td>

</tr>



<tr>

<td><span class="code">{n,m}</span></td>

<td><span class="desc">重复n到m次</span></td>

</tr>

</tbody>

</table>

#3.常用的反义代码

<table cellspacing="0">

<thead>

<tr>

<th scope="col">代码/语法</th>



<th scope="col">说明</th>

</tr>

</thead>

<tbody>

<tr>

<td><span class="code">\W</span></td>

<td><span class="desc">匹配任意不是字母，数字，下划线，汉字的字符</span></td>



</tr>

<tr>

<td><span class="code">\S</span></td>

<td><span class="desc">匹配任意不是空白符的字符</span></td>

</tr>

<tr>

<td><span class="code">\D</span></td>



<td><span class="desc">匹配任意非数字的字符</span></td>

</tr>

<tr>

<td><span class="code">\B</span></td>

<td><span class="desc">匹配不是单词开头或结束的位置</span></td>

</tr>

<tr>



<td><span class="code">[^x]</span></td>

<td><span class="desc">匹配除了x以外的任意字符</span></td>

</tr>

<tr>

<td><span class="code">[^aeiou]</span></td>

<td><span class="desc">匹配除了aeiou这几个字母以外的任意字符</span></td>

</tr>



</tbody>

</table>


    







   