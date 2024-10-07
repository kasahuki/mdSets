<center><b><font size=60 color=green  >Regular Experssion</font></b></center>

`use to match`

**应用：网站域名url 以及 html标签  或者 rgba?属性**   或者 ipv4地址

（重要在于实践）

# ==限定符（Quantifiers）==

## ？ 

`e.g.  used?  表示前面这个单词出现0到1词（0/1）`

## *

`b*  : 表示b这个字符只能出现0次以上`

## +

表示出现1次以上

## {}

**a{5}  : 表示出现特定（specify）次数**

**a{3,6} : 表示出现 范围   -->  a{2，（可省略）} 表示出现2次以上!**



## ()

类似与多个字符绑定使用--> 字符组

e.g.  (ab)+ : 表示 ab出现 1 次以上



## 或运算

符号使用： | 

e.g. a (cat|dog)  （一定不能少了这个括号）

## []

**e.g. [01] 就表示01集合**

方括号里的内容代表要求匹配的字符只能取自里面

==也就是一个集合，这个位置上必须要是取自集合里的东西！！！==

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922211910573.png" alt="image-20240922211910573" style="zoom: 50%;" />

**就相当于是取并集--->都可以!!**



## 脱字符 ^ (相当于取反集合)

e.g.   【^0-9】 表示所有的非数字字符（空白字符，特殊符号）

# ==元字符(Meta - characters)==

==大多数都以**反斜杠**开头==



|               \d 数字字符                |   \D 非数字字符   |
| :--------------------------------------: | :---------------: |
| **\w 单词字符（英文、数字、下划线……）**  | **\W 非单词字符** |
| \s 空白字符（包含tab，和换行符，空格……） |       同理        |





## .与.*

![image-20240922213523493](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922213523493.png)

# ==锚点==(一般是匹配位置（就是一个边界线）而不是具体字符！)

## \b 表示单词字符的边界(\B 表示非单词字符的边界) 边界是指边界<font color='red'>线</font>！

**边界就是一个状态到另一个状态的临界点！！**

e.g. **|**hello**|**world

![image-20240922225244737](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922225244737.png)

<font size="40">**实例：**</font>



<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922230229195.png" alt="image-20240922230229195" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922230243980.png" alt="image-20240922230243980" style="zoom:50%;" />

## ^匹配行首 $ 匹配行尾

e.g. 

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922213959412.png" alt="image-20240922213959412" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922213955188.png" alt="image-20240922213955188" style="zoom:50%;" />

## 贪婪匹配&& 懒惰匹配（加个问号转化为非贪婪模式，钝化）



![image-20240922214325440](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922214325440.png)

==尽可能去匹配更多的字符==



![image-20240922214341277](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922214341277.png)

==反之==

## ==！注意 问题 ！==

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922215154506.png" alt="image-20240922215154506" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922215212363.png" alt="image-20240922215212363" style="zoom:50%;" />

# ==转义字符==

![image-20240922222058615](https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922222058615.png)

\r 表示 回车 就是 将光标移到 该行的开头不换行！！



## 注意也有转义字符的概念（即：以反斜杠开头的）

## `\. 就表示 . 这个字面量！！！`





# REGEX FLAGS



<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922221535701.png" alt="image-20240922221535701" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922221542411.png" alt="image-20240922221542411" style="zoom:50%;" />

<img src="https://cdn.jsdelivr.net/gh/kasahuki/os_test@main/img/image-20240922221557445.png" alt="image-20240922221557445" style="zoom:50%;" />





