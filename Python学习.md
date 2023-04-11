# Python学习

[TOC]



- 学习路线（基础阶段）：

  Python基础语法，标识符、关键字、变量、判断循环

  容器类型（数据类型中的高级类型）

  函数

  文件处理

  面向对象

  包和模块

  异常处理

## 一、Python基础

创始人：吉多·范罗苏姆(Guido van Rossum)，龟叔

### 1、入门阶段

#### Python解释器、Pycharm

- Python解释器

作用：运行Python语言，.py文件 -> Python解析器 -> 机器语言

CPython，C语言开发的解释器（官方），应用最广泛

JPython，运行在Java平台的解释器，直接把Python代码编译成Java字节码执行，极大提升了执行效率，但是增加了编译时间。

- Pycharm

一种Python IDE（集成开发工具），Python开发工具。

#### 变量、注释

- 注释

```python
# 单行注释  注释内容

"""
Python不区分单双引号
所以用单引号也能多行注释
注释1
注释2
...
"""

'''
注释
注释
...
'''
 
# ctrl + /  注释快捷键
```

多行注释无法用在语句末尾



- 变量

> 变量是存储数据的容器
>
> 变量在程序运行过程中可以改变的
>
> 变量存储的数据是临时的
>
> 变量名 = 变量的值
>
> 变量必须先定义再调用



标识符命名规则（必须遵守）：

① 由数字、字母、下划线组成

② 不能数字开头

③ 严格区分大小写

④ 不能使用内置关键字作为变量名称



标识符命名规范：

① 变量命名一定要做到见名知义

② 大驼峰：即每个单词首字母都大写，例如：MyName；Python中多用于类名

③ 小驼峰：第二个（含）以后的单词首字母大写，例例如：myName

④ 下划线：例如：my_name；Python中用于命名变量、函数、文件名、包和模块名



- 变量的数据类型

  Python中数据类型只有7种

  数值型：int整型、float浮点型

  布尔型：true、false

  字符串：str

  列表：list  [ ]

  元组：tuple  ( )

  集合：set  { }

  字典：dict  { ' ' : ' ' }

```python
# 查看数据类型的函数：type(数据/变量名)
int1 = 12
print(type(int1))  # <class 'int'>
```

变量和字符串的区别：

```python
# 定义一个变量
name = xiaoming

# 打印输出
print(name)  # xiaoming 
print('name')  # name
```



#### Bug和Debug

- bug

  三步法：

  ① 查错误文件

  ② 查行号

  ③ 查看错误描述

  

- Debug调试工具：逐步执行代码，可查看与分析Python解析器是如何解析Python代码的

  使用：①打断点；②启动Debug调试

  对于简单的代码我们可以直接在第一行添加一个断点；对于复杂的程序，有逻辑关键字如if/while/for等等，断点必须添加到关键字的前面



### 2、输入和输出

#### print输出

普通输出变量：print

Pycharm中直接输入：name.print后软件会自动将其转换为print(name)

#### 百分号格式化输出

%格式如下：其中前三个很常用

| **格式符号**（占位符） | **转换**               |
| ---------------------- | ---------------------- |
| ==%s==                 | 字符串                 |
| ==%d==                 | 有符号的十进制整数     |
| ==%f==                 | 浮点数                 |
| %c                     | 字符                   |
| %u                     | 无符号十进制整数       |
| %o                     | 八进制整数             |
| %x                     | 十六进制整数（小写ox） |
| %X                     | 十六进制整数（大写OX） |
| %e                     | 科学计数法（小写'e'）  |
| %E                     | 科学计数法（大写'E'）  |
| %g                     | %f和%e的简写           |
| %G                     | %f和%E的简写           |

语法

```python
print(变量名称)
print('字符串%格式' % (变量名称))
print('字符串%格式 %格式 %格式' % (变量名称1, 变量名称2, 变量名称3))
```

使用

```python
# 定义变量
name = 'Connor'
age = 18
address = 'shanghai'

# 输出变量（普通输出）
print(name)
print(age)
print(address)

# 百分号格式化输出
print('My name is %s, I am %d years old.' % (name, age))

# 案例：定义两个变量title=大白菜，price=3.5.按照如下格式进行输出：今天蔬菜特价了，大白菜只要3.5元／斤。
title = '大白菜'
price = 3.5

print('今天蔬菜特价，%s只要%f元/500g' % (title, price))  # 会输出3.500000，float默认保留6位小数
print('今天蔬菜特价，%s只要%.1f元/500g' % (title, price))  # 将需要保留的位数写在格式前方，.1表示保留1位小数

# 案例：定义两个变量id=1，name='Connor'，按照如下格式进行输出：姓名：Connor，学号：000001
id = 1
name = 'Connor'

print('姓名：%s，学号：%06d' % (name, id))  # 格式前的数字表示需要保留多少位，06表示保留6位数，不足6位就用0填充

# 案例：由于受到俄罗斯与乌克兰战争影响，原油价格上浮5%！
num = 5
# print('由于受到俄罗斯与乌克兰战争影响，原油价格上浮%d%！' % (num))
print('由于受到俄罗斯与乌克兰战争影响，原油价格上浮%d%%！' % (num))

```

 

#### format方法实现格式化输出

只能在Python3中使用

语法：

```python
print('字符串{}'.format(变量名称1))
print('{}字符串{}'.format(变量名称1, 变量名称2))
```

使用

```python
# format方法只能在Python3中使用
# 案例：定义两个变量，name='孙悟空'，mobile = '18700000000'，按照以下格式进行输出"姓名；孙悟空，联系方式：18700000000"
name = '孙悟空'
mobile = '18700000000'
print('姓名：{}，联系方式：{}'.format(name, mobile))
```



#### format方法简写形式格式化输出（推荐）

在Python3.6及以后版本中才能使用

语法

```python
print(f'字符串：{变量名1}，字符串：{变量名2}')
```

使用

```python
# format方法只能在Python3中使用
# 案例：定义两个变量，name='孙悟空'，mobile = '18700000000'，按照以下格式进行输出"姓名；孙悟空，联系方式：18700000000"
name = '孙悟空'
mobile = '18700000000'
print('姓名：{}，联系方式：{}'.format(name, mobile))

# format方法简写形式格式化输出（推荐）,在Python3.6及以后版本中才能使用
print(f'姓名：{name}，联系方式：{mobile}')

# 案例：定义两个变量title=大白菜，price=3.5.按照如下格式进行输出：今天蔬菜特价了，大白菜只要3.50元／斤。
title = '大白菜'
price = 3.5
print('特价，{}只要{:.2f}元/斤'.format(title, price))
print(f'特价，{title}只要{price:.2f}元/斤')  # 保留2位小数

# 案例：定义两个变量id=1，name='Connor'，按照如下格式进行输出：姓名：Connor，学号：000001
id = 1
name = 'Connor'
print('姓名：{}，学号：{:06d}'.format(name, id))
print(f'姓名：{name}，学号：{id:06d}')  # 保留6位数，不够就补0

```



#### 格式化输出中的转义字符

\t：制表符，等价于一个Tab键或4个空格

\n：换行符，等价于一个回车，\n之后的内容会换行

```python
# 转义字符 \t  \n
'''
输出以下内容
        *
    *   *   *
*   *   *   *   *
'''

print('\t\t*')
print('\t*\t*\t*')
print('*\t*\t*\t*\t*')

print('\t\t*\n\t*\t*\t*\n*\t*\t*\t*\t*')
```

#### input输入

用于接收由外部设备输入的内容，但是如果程序只有input()其实没有任何意义，我们一般拿到这个数据以后，还需要进一步加工，所以建议定义一个变量保存用户的输入内容

> input()内的内容永远都是str字符串类型
>
> input()具有一个"暂停"功能，即阻塞后续代码的执行，直到用户输入完成以后，代码才可以继续向下执行

基本语法：

变量名称 = input('代表提示用户输入信息：')

```python
# 输入密码 展示密码
num = input('请输入密码：')
print('请确认密码：', num)
```

### 3、运算符

字符串与数字相乘是将字符串复制乘数的份数

#### 数据类型转换

| **函数**                 | **说明**                                                     |
| ------------------------ | ------------------------------------------------------------ |
| ==int(x)==               | 将x转换为一个整数                                            |
| ==float(x)==             | 将x转换为一个浮点数                                          |
| complex(real  [,imag  ]) | 创建一个复数，real为实部，imag为虚部                         |
| ==str(x)==               | 将对象 x  转换为字符串                                       |
| repr(x)                  | 将对象  x  转换为表达式字符串                                |
| ==eval(str)==            | 用来计算在字符串中的有效Python表达式,并返回一个对象（字符串中的数据像什么就转换成什么类型） |
| tuple(s)                 | 将序列 s  转换为一个元组                                     |
| list(s)                  | 将序列 s  转换为一个列表                                     |
| chr(x)                   | 将一个整数转换为一个Unicode字符                              |
| ord(x)                   | 将一个字符转换为它的ASCII整数值                              |
| hex(x)                   | 将一个整数转换为一个十六进制字符串                           |
| oct(x)                   | 将一个整数转换为一个八进制字符串                             |
| bin(x)                   | 将一个整数转换为一个二进制字符串                             |

用法

```python
# 字符串的四则运算
str1 = 'hello'
print(str1 * 2)  # 字符串与数字相乘是复制字符串

# 数据类型转换
str1 = '10'
# str => int
num1 = int(str1)
print(num1, type(num1))

# float => int
float1 = 12.99
num2 = int(float1)
print(num2, type(num2))  # 将浮点数转换成整数时会损失小数部分

# float => str
str2 = str(float1)
print(str2, type(str2))

# str => eval => int
num3 = eval(str1)
print(num3, type(num3))

# str => eval => float
str3 = '12.999'
num4 = eval(str3)
print(num4, type(num4))

# str => float => int
# num5 = int(str3) 直接将看似浮点类型的字符串转换为整数会报错
num5 = float(str3)
num5 = int(num5)
print(num5, type(num5))
```

#### 算数运算符

| **运算符** | **描述**     | **实例**                                                 |
| ---------- | ------------ | -------------------------------------------------------- |
| +          | 加           | 1 +  1 输出结果为  2                                     |
| -          | 减           | 1 -  1 输出结果为  0                                     |
| *          | 乘           | 2 *  2 输出结果为  4                                     |
| /          | 除           | 10  / 2 输出结果为  5                                    |
| //         | 整除         | 9  // 4 输出结果为  2                                    |
| %          | 取余（取模） | 9 %  4 输出结果为  1                                     |
| **         | 幂指数       | 2  ** 4 输出结果为  16，即2的4次方，2  * 2 * 2 * 2       |
| ()         | 小括号       | 小括号用来提高运算优先级，即  (1  + 2) * 3 输出结果为  9 |

```python
num1 = 9
num2 = 4

# 运用所有算数运算符进行计算
print(num1 + num2)
print(num1 - num2)
print(num1 * num2)
print(num1 / num2)  # 返回的值一定是浮点型
print(num1 // num2)
print(num1 % num2)
print(num1 ** num2)
print((num1 + num2) - num1)
```



#### 赋值运算符 = 

将等号右边的值或者表达式的执行结果赋值给左边的变量

执行流程是从右到左

变量名称 = 变量的值或者运算表达式

```python
# 单个赋值
num = 10

# 多个变量同时赋值
a, b, c = 2, 3, 5

# 为多个变量赋予相同的值
num1 = num2 = 6
```



#### 复合赋值运算符

先运算后赋值，符号左边必须是变量

| **运算符** | **描述** | **实例**                 |
| ---------- | -------- | ------------------------ |
| +=         | 加法赋值 | c += a等价于c = c + a    |
| -=         | 减法赋值 | c -= a等价于c = c - a    |
| *=         | 乘法赋值 | c *= a等价于c = c * a    |
| /=         | 除法赋值 | c /= a等价于c = c / a    |
| //=        | 整除赋值 | c //= a等价于c = c // a  |
| %=         | 取余赋值 | c %= a等价于c = c % a    |
| **=        | 幂赋值   | c * *= a等价于c = c ** a |



#### 比较运算符

返回结果是一个bool类型的数据

| ==   | 判断相等。如果两个操作数的结果相等，则条件结果为真（True），否则条件结果为假（False） | 如a=3，b=3，则（a==b）为True                              |
| ---- | ------------------------------------------------------------ | --------------------------------------------------------- |
| !=   | 不等于。如果两个操作数的结果不相等，则条件为真（True），否则条件结果为假（False） | 如a=3，b=3，则（a==b）为True如a=1，b=3，则（a！=b）为True |
| >    | 运算符左侧操作数结果是否大于右侧操作数结果，如果大于，则条件为真，否则为假 | 如a=7，b=3，则（a>b）为 True                              |
| <    | 运算符左侧操作数结果是否小于右侧操作数结果，如果小于，则条件为真，否则为假 | 如a=7，b=3，则（a<b）为False                              |
| >=   | 运算符左侧操作数结果是否大于等于右侧操作数结果，如果大于，则条件为真，否则为假 | 如a=7，b=3，则（a>= b）为 True                            |
| <=   | 运算符左侧操作数结果是否小于等于右侧操作数结果，如果小于，则条件为真，否则为假 | 如a=3，b=3，则（a<=b）为 True                             |



#### 逻辑运算符

![image-20210307144233542](images/image-20210307144233542.png)

- 短路运算（and、or）

  如果逻辑运算符左边的表达式结果满足短路法则的条件则运算符右边表达式不需要执行，直接输出结果（==谁决定了这个表达式的最终结果，则表达式就返回谁==）

  可加快程序的执行

  ==0、空字符串、None看作False，其他数值和非空字符串都看作True==

#### 运算符优先级

![image-20210708111605748](images/image-20210708111605748.png)

> 先算乘除，后算加减，有括号的先算括号里面的。
>
> ① 不要把一个表达式写得过于复杂，如果一个表达式过于复杂，尝试把它拆分来书写
>
> ② 不要过于依赖运算符的优先级来控制表达式的执行顺序，这样可读性太差，应尽量使用( )来控制表达式的执行顺序



### 4、if选择结构

基本结构

```python
if True:
    print('条件成立执行的代码1')
    print('条件成立执行的代码2')

# 下方的代码没有缩进到if语句块，所以和if条件无关
print('我是无论条件是否成立都要执行的代码')
```

用法

```python
# 简单判断
age = 19
if age >= 18:
    print('已成年')
print('成年请进，未成年禁止通过')

# 通过输入来判断
age = int(input('请输入您的年龄：'))
if age >= 18:
    print('pass')
print('成年请进，未成年禁止通过')
```



#### if...else结构：二选一结构

if条件判断：

​	条件判断成立，则执行if中的缩进代码

else：
	如果条件不成立，则执行else中的缩进代码

```python
age = int(input('请输入您的年龄：'))
if age >= 18:
    print('pass')
else:
    print('fail')
```

#### Visio流程图绘制

- 流程图图形含义

  椭圆形：程序的开始或者结束

  矩形：代表程序执行到某个流程，普通流程

  菱形：判断逻辑，填写判断条件

#### if...elif...else多分支结构

```python
if 条件判断1:
	若条件判断1成立，则执行if中的缩进代码

elif 条件判断2:
	条件判断1不成立，条件判断2成立，则执行elif中的缩进代码

elif 条件判断3:
	若条件判断1不成立，条件判断2也不成立，条件判断3成立，则执行elif中的缩进代码

...

elif 条件判断n:
	若之前的条件都不成立，条件判断n成立，则执行elif中的缩进代码

else:  # else结构可以不用
	如果所有条件都不成立，则执行else中的缩进代码
```

#### if嵌套结构

```python
if 外层条件判断:
    # 如果条件为True，则执行以下语句段
    if 内层条件判断:
        # 如果内层条件为True，则执行以下语句段
else:
    # 如果条件为False，则执行以下语句段
```

==先编写外层判断，所有语句编写完成后，再编写内层条件判断结构.==

#### if结构综合案例

```python
# 随机模块的使用
# 1. 导入模块
import random  
# 2. 基于模块中的randint(start, stop)闭区间，规定随机数范围
randnum = random.randint(0, 2)  # 0, 1, 2
print(randnum)
```



```python
# 参与游戏的角色有两个（玩家 与 电脑，人机对战），玩家手工出拳，电脑随机出拳，根据石头剪刀布判断输赢。
# 玩家：player（玩家手工输入石头0、剪刀1、布2）
# 电脑：computer（随机出拳）
# 1. 导入模块
import random
computer = random.randint(0, 2)
# 2. 基于模块中的randint(start, stop)闭区间，规定随机数范围
player = int(input('请出拳（玩家手工输入石头0、剪刀1、布2）：'))
print(f'电脑出拳：{computer}')
if (player == 0 and computer == 1) or (player == 1 and computer == 2) or (player == 2 and computer == 0):
    print('player win')
elif player == computer:
    print('no winner')
else:
    print('player lose')
```

#### 三目运算符（三元运算符）

用于简化if...else语句

```PYTHON
# 传统语法
if 条件判断：
	条件判断成立，则执行if中的缩进代码
else：
	如果条件不成立，则执行else中的缩进代码

# 三目运算符语法
值1 if 条件判断 else 值2
# 如果条件判断成立，则返回值1，若条件不成立，则返回else中的值2
```

案例：求两个数中的最大值

```python
# 求最大值
import random
num1 = random.randint(1, 100)
num2 = random.randint(1, 100)
maxnum = num1 if num1 > num2 else num2
print(f'num1 = {num1}, num2 = {num2}, maxnum = {maxnum}')
```



### 5、循环结构

让代码高效重复执行，循环结构有while和for两种

对于循环次数已知的情况，适合使用while循环，因为while循环有计数器

对于循环次数未知的情况，如数据容器（字符串、列表、元组、字典、集合统称数据容器）的遍历，推荐使用for循环

所以for循环其实是专门用于实现对数据容器的遍历操作

#### while循环

- 使用方法

  ① 定义一个计数器

  ② 编写一个循环条件

  ③ 在循环体内部（1个缩进）更新计数器的值

```python
# 例1：循环打印1-5
i = 1
while i <= 5:
    print(i)
    i += 1
# 例2：求1-100的和
i = 1
sum = 0
while i <= 100
	sum += i
	i += 1
print(sum)
# 例3：求1-100中偶数的和
i = 1
sum = 0
while i <= 100
	if i % 2 == 0:
		sum += i
	i += 1
print(sum)
```

#### while循环中的常见关键词

break和continue是循环中满足一定条件退出循环的两种不同方式

break：一旦循环中执行了break关键字就终止整个循环

continue：在循环中执行continue后，将回到循环条件处重新开始执行，即中止本次正在执行的循环，继而进入下一次循环结构

> 注意：在使用continue的循环中，continue语句之前需要更新计数器，否则会出现死循环

```python
# 吃5个苹果案例
# break 吃到第四个吃饱了
i = 1
while i <= 5:
    if i == 4:
        print('吃饱了不吃了')
        break  # 终止整个循环
    print(f'正在吃第{i}个苹果')
    i += 1
# continue 第3个苹果坏了，跳过第三个，接着吃完苹果
i = 1
while i <= 5:
    if i == 3:
        print('这个苹果坏了，不吃')
        i += 1  # 不增加计数器的值就会死循环
        continue  # 跳出第三次循环开始第四次
    print(f'正在吃第{i}个苹果')
    i += 1
```

#### 死循环

两种死循环：

① 程序编写错误出现的死循环

② 人为设计的死循环

死循环本身没有任何意义，如果想要死循环有意义必须要结合input()输入语句

```python
# 通讯运营商电话选项模拟,引入input打断死循环
while True:
    print('欢迎致电XXXXX，请按照语音提示输入号码')
    print('按1查询话费余额')
    print('按2查询宽带余额')
    print('按3查询已办理业务')
    print('按0进入人工服务')
    usernum = input('请输入号码：')
```

#### while循环案例

猜数字

需求：

① 计算机从1 ~ 10之间随机生成一个数字，然后提示输入数字，如果我们输入的数字与随机数相等，则提示恭喜你，答对了。如果输入的数字比随机数大，则提示，猜大了。反之，则提示猜小了，一共有3次机会。

② 无限次猜测机会

```python
# 需求：计算机从1 ~ 10之间随机生成一个数字，
# 然后提示输入数字，如果我们输入的数字与随机数相等，则提示恭喜你，答对了。
# 如果输入的数字比随机数大，则提示，猜大了。
# 反之，则提示猜小了，一共有3次机会。
import random
i = 1
while i <= 3:
    randnum = randint(1, 10)
    usernum = int(input('请输入数字猜谜：'))
    if usernum == randnum:
        print('猜对了')
    elif usernum > randnum:
        print('猜大了')
    else:
        print('猜小了')
    i += 1

# 改良猜谜，不限制次数
import random
randnum = random.randint(1, 10)
while True:  # 无限次循环猜谜
    usernum = int(input('请输入数字进行猜谜：'))
    if randnum == usernum:
        print('猜对了')
        break  # 猜对后终止
    elif randnum > usernum:
        print('猜小了')
    else:
        print('猜大了')

```



#### for循环

专门用于实现对数据容器的遍历

```python
# 语法
for 临时变量 in 数据容器：
	print（临时变量）
执行原理：
①首先判断数据容器中有多少个元素，则for循环就要循环多少次
②每次循环时，系统会自动将遍历得到的字符放入临时变量（临时变量一般起名叫i）中，打印这个变量就相当于输出字符串中的每一个字符
    
# 举例
# 遍历字符串，打印每个字母
for i in 'xiaobang'
	print(i)
```



#### range()方法

问题：for循环也是循环，能不能实现固定循环多少次，比如循环10次

答：默认情况下，for循环只能用于遍历数据容器。但是如果一定想要达到这个效果，可以使用range（）方法

range（）方法可以用于生成指定长度的容器=>类似[1, 2, 3]

range（）基本语法range（start, stop, step）

参数说明：

start代表起始值，从哪里开始生成

stop代表结束值，到哪里结束，不包含结束值（只顾头不顾尾） 

step代表步长，代表每次前进多少个元素，默认值为1

```python
# 使用for循环求1-100的和，range方法
sum = 0
for i in range(1, 101, 1)
	sum += i
print(sum)
# 使用for循环求1-100中的偶数和
sum = 0
for i in range(2, 101, 2)
	sum += i
print(sum)
# 或者
sum = 0
for i in range(101)
	if i % 2 == 0
    	sum += i
print(sum)
```

#### for循环案例

```python
# 案例：用for循环实现用户登录
# ①输入用户名和密码
# ②判断用户名和密码是否正确
# ③登录仅有三次机会，超过3次会报错
# ④如果用户登录失败，则提示用户名错误还是密码错误
# ⑤获取剩余的登录次数
name = 'admin'
key = 'admin1234'
for i in range(3):
    username = input('请输入账号：')
    password = input('请输入密码：')
    if username == name:
        if password == key:
            print('登录成功')
            break
        else:
            print('密码错误，请重新输入')
            print(f'剩余{2 - i}次错误机会')
    else:
        print('账号错误，请重新输入')
        print(f'剩余{2 - i}次错误机会')
else:
    print('错误次数超过限制，请30分钟后重试')
```

#### 循环的else结构

Python的特殊用法，其余大部分语言的while/for循环无法使用else

else下方缩进的代码指的是==当循环正常结束之后要执行的代码。==

强调：'正常结束'，非正常结束，其else中的代码时不会执行的。（如遇到break的情况）

基本语法：

```python
while 循环条件:
    循环体
else:
    当循环正常结束后，需要执行的代码

for 临时变量 in 序列:
    循环体
else:
    当循环正常结束后，需要执行的代码
```

简单用法

```python
# 打印字符串xiaobang并正常执行else后的代码
for i in 'xiaobang'
	print(i)
else:
    print('打印完毕')
# 遇到break时
for i in 'xiaobang'
	if i == 'b':
        print('break')
        break
	print(i)
else:
    print('打印完毕')
```



#### for循环综合案例

报数字游戏，数7游戏

规则：一些同学从1开始报数，当需要报出的数字尾数是7或者该数字是7的倍数时，则该同学跳过这个数字，不进行报数。所有同学都参与游戏后，游戏结束。如输入学生数量为50，游戏结束后，报数的同学数量为39。

```python
count = 0
stunum = int(input('请输入学生数量：'))
for i in range(1, stunum + 1):  # range顾头不顾尾，并且必须从1开始报数
    if i % 7 == 0 or i % 10 == 7:  # 逢7必过
        continue
    else:
        count += 1  # 统计报数的人
print(f'报数的学生数量为：{count}')
```



### 6、数据容器

#### 字符串

用单引号或者双引号包围的数据。

可以使用三引号来定义字符串，定义字符串后必须要赋值，三引号内的字符串支持换行操作

```python
# 不换行
str1 = '这是一行字符串'
print(str1)
print(type(str1))

# 换行
str2 = '''
	这是
	很多行
	字符串
'''
print(str2)
print(type(str2))

# 定义特殊字符串，例如：I'm Connor.
# 字符串中若包含引号，可以使用以下方法来定义：
# ①交叉定义，比如里面是单引号，外面就使用双引号
# ②使用反斜杠\转义字符，对引号进行转义
print("I'm Connor")
print('I\'m Connor')
```

> 在计算机底层，字符串存储在一段连续的内存地址中，每个字符单独存储，每个字符都有一个索引。第一个字符的索引是0

```python
# 通过索引输出字符串的字符
str3 = 'xiaobang'
print(str3[0])
print(str3[1])
print(str3[2])
```

#### 切片

切片是指对操作的对象截取其中一部分的操作。字符串、列表、元组都支持切片操作。

- 语法

  ```pythoon
  序列[start:stop:step]
  ```

  步长step默认为1，start和stop是开始和结束索引，start默认为0

  没有start代表从第0个元素开始截取，没有stop表示截取完最后一个元素

- 使用切片的小技巧

  ① 绘制图像（画格子，一个元素一个格子）

  ![image-20210310110051093](images\image-20210310110051093.png)

  ② 记住切片口诀

  ==先看步长后头尾，步长为正正向移，步长为负逆向移，只顾头来尾不管==

```python
numstr = '0123456789'
# 截取234
print(numstr[2:5:1])
print(numstr[2:5])
print(numstr[-8:-5])
print(numstr[-6:-9:-1])  # 反向
# 0123
print(numstr[:4])  # start默认为0
print(numstr[:-6])  # 不加step默认为1
# 123456789
print(numstr[1:])  # stop默认为最后一个索引+1
# 543210
print(numstr[5::-1])
# 截取整个字符串
print(numstr[::])
# 字符串翻转
print(numstr[::-1])
# 截取所有偶数或奇数
print(numstr[::2])
print(numstr[-2::-2])
print(numstr[1::2])
print(numstr[-1::-2])
```

> 如果切片方向与步长方向相反，则截取不到任何数据

#### 字符串常用操作方法

Python内置的方法

##### 字符串查找find()

语法

```python
字符串.find(要查找的字符或者子串:start:stop)
# start和stop可以不填，那就检查整个字符串
# 找到内容就返回子串的开始索引，找不到就返回-1
```

案例

```python
# 定义一个字符串
str1 = 'hello world hello linux hello python'
# 查找linux子串是否出现在字符串中
print(type(str1.find('linux')))  # 返回int18，即linux开始的索引
print(str1.find('linux'))
# 在str1中查找不存在的子串
print(str1.find('aaaaaaa'))  # 返回-1，不存在该子串

file = input('请输入您要上传文件的名称：')  # 假如输入avatar.png
# 获取点号的索引下标
index = file.find('.')
print(index)
# 求文件名称filename
filename = file[:index]
print(filename)
# 求文件后缀postfix
postfix = file[index:]
print(postfix)
```

##### 字符串修改

replace()：把某个关键词进行替换，返回替换后的内容

split()：对字符串进行切割操作，返回一个列表

join()：和split()正好相反把列表容器合并为字符串

语法：

```python
replace(old, new)  # 把字符串中的关键词进行替换
split(分隔符号)  # 使用分割符号对字符串进行切割,返回一个列表,列表中的每一个元素就是分隔符两边的数据
join(列表容器)  # 把一个列表在拼接为字符串
```

案例：

```python
str1 = 'hello linux and hello linux'
# 把字符串中所有linux字符替换为python
print(str1.replace('linux', 'python'))
# 把字符串中的第一个linux进行替换为python
print(str1.replace('linux', 'python', 1))  # 可指定替换哪一个子串，不指定就是替换全部
# 把and字符串替换为&&
print(str1.replace('and', '&&'))
# 字符串切割
str2 = 'apple-banana-orange'
print(str2.split('-'))  # 切割符号在后
# 序列拼接
list1 = ['apple', 'banana', 'orange']
print('-'.join(list1))  # 拼接符号在前
```

##### 字符串判断

isdigit()：判断一个字符串是否全部由纯数字组成，纯数字返回True，反之返回False

```python
# 输入字符串并判断是否是纯数字，是则返回数字，反之返回error
user_input = input('请输入数字：')
if user_input.isdigit():
    print(user_input)
else:
    print('error，请输入数字')
```



#### 列表

一个列表容器中可以保存多个数据，且这些数据可以是不同的数据类型，列表内的数据可以修改

```python
列表名称 = [元素1, 元素2, 元素3, ...]
```

举例：

```python
# 定义列表names
names = ['Tom', 'Lily', 'Lihua', 'Connor']
print(names)
print(type(names))
```

#### 列表的常用操作方法

##### 查询

列表中的每一个元素都有一个索引，可通过以下语法访问列表中的指定元素：

```python
列表名称[索引]  # 语法
# 访问列表内元素
print(names[0])
print(names[3])
print(len(names))  # len()用于求字符或数据容器的长度

# 遍历列表
i = 0
while i < len(names):
    print(names[i])
    i += 1

for i in names:
    print(i)
```

in判断方法，判断某个元素是否出现在数据容器当中，可以用于多个数据容器

```python
if 元素 in 数据容器:  # 判断元素是否出现在容器中，如果出现，则返回True，没有出现，则返回False

black_ip = ['192.168.89.77', '222.246.129.81', '172.16.54.33']
if '192.168.89.77' in black_ip:
    print('IP被锁定，禁止访问')
else:
    print('正常访问')
    
# 字符串中的in方法
str1 = 'hello python'
if 'py' in str1:
    print('py在str1中')
else:
    print('py不在str1中')
```

##### 增加

append()，在列表的尾部追加元素，不返回任何数据

+加号：合并列表

```python
# 添加元素进列表 append
list1 = ['刘备', '曹操']
list1.append('孙权')
print(list1.append('孙权'))  # 不返回任何值
print(list1)

# 合并列表 +
list2 = ['Tom', 'Lily']
list3 = ['Connor', 'Jony']
print(list2 + list3)
```

##### 删除

remove()，根据元素值删除元素

```python
# 删除列表中的元素，remove
list1.remove('曹操')
print(list1.remove('曹操'))  # 不返回任何元素
print(list1)
```

##### 修改

```python
列表名称[索引] = 新元素  # 修改列表中指定元素
# 修改元素
list1[1] = '曹孟德'
print(list1)
```

##### 翻转与排序

reverse()，翻转列表中元素的顺序，相当于切片中的[::-1]

sort()，对数值排序，默认从小到大排列。添加参数：reverse = True，从大到小排序；reverse = false，从小到大排序

```python
# 翻转和排序，两者都不返回任何元素，需要打印列表
# reverse翻转，用切片也可以实现
list4 = ['5', '3', '2', '1', '7', '9']
list5 = ['刘备', '关羽', '张飞']

list5.reverse()
print(list5)
print(list5[::-1])

list4.sort()
print(list4)
list4.sort(reverse=True)
print(list4)
```

##### 列表嵌套

```python
# 基本语法
列表名称 = [[], [], []]

# 举个栗子：假设我们有三个班级，分别为一班、二班、三班
# 1：Tom, Jack, Harry
# 2班：小明，小红，小绿
# 3班：刘备，关羽，张飞
# 如何实现保存以上信息
students = [['Tom', 'Jack', 'Harry'], ['小明', '小红', '小绿'], ['刘备', '关羽', '张飞']]
# 获取'小红'
print(students[1][1])                                                                                   
```

#### 元组

使用小括号和逗号，数据可以是不同的数据类型，==元组内存储的数据无法修改==，而列表可以修改

```python
# 基本语法
元组名称 = (元素1, 元素2, 元素3)

# 定义一个只含一个元素的元组（特殊）
tuple1 = (10,)  # 如果定义的元组是一个单元素元组，则最后必须保留一个逗号，否则定义的就不是元组类型了！
print(type(tuple1))
tuple0 = (10)
print(type(tuple0))

# 多元素元组
tuple2 = (10, 20, 30, 40)
print(type(tuple2))

# 打印元组
print(tuple2)
# 遍历元组
for i in tuple2:
    print(i)
# 通过索引访问元组的元素
print(tuple2[0])
print(tuple2[3])
```

##### 元组的应用场景

- 函数的参数和返回值，一个函数可以接受任意多个参数，或者依次返回多个数据(了解)

  def func(参数1, 参数2, 参数3):

  ​	  return 返回值1, 返回值2, 返回3

- 格式化字符串，百分号和format，格式化字符串后面的（）本质上就是一个元组

  print('姓名：%s，年龄：%d，家庭住址：%s'  %  (name, age, address))

- 让列表不可以修改，以保护数据安全

- python操作mysql数据库，返回结果，默认也是元组类型

##### 元组的操作方法，查询

由于元组中的数据不允许直接修改，所以其操作方法大部分为==查询方法==。

| **编号** | **函数**   | **作用**                 |
| -------- | ---------- | ------------------------ |
| 1        | 元组[索引] | 根据==索引下标==查找元素 |
| 2        | len()      | 统计元组中数据的个数     |
| 3        | in         | 判断元素是否出现在元组中 |

```python
tuple1 = (10, 20, 50, 40, 90)
# 索引
print(tuple1[1])
print(tuple1[3])
print(tuple1[0])
# len方法
print(len(tuple1))
# in条件判断
if 50 in tuple1:  # 判断元组中是否包含50
    print('50 exists in the tuple')
else:
    print('50 not exists in the tuple')
```



#### 字典

在Python中，字典（Dictionary）是一种无序、可变的数据结构，用于存储键值对（key-value pairs）。

注意事项：字典中是没有索引下标的，其是通过key:value键值对来体现键（等价于索引下标）与值的关系

key：键名，必须是唯一的且没有顺序要求，其可以是字符串类型、数字化类型或者元组类型

value：代表的字典中具体的元素值。

字典使用花括号 {} 定义，键和值之间使用冒号 : 分隔，每个键值对之间使用逗号 , 分隔。

```python
# 语法
字典名称 = {key1:value1, key2:value2, key3:value3}

# 定义空字典
dict1 = {}
print(type(dict1))
dict1 = dict()
print(type(dict1))
# 定义并输出一个非空字典，存储：'Tom', 'male', 20
person = {'name':'Tom', 'gender':'male', 'age':20}
print(person)
# 访问字典中某个具体的value值
print(person['name'])
print(person['age'])
```

存储方式：

![image-20210602110608215](images\image-20210602110608215.png)

注意：

① 字典没有切片操作

② 创建有数据的字典只能使用{}方法，不能使用dict()方法

③ 无论key还是value，遵循一个原则：如果是字符串类型，则添加引号；如果是数值类型，则不需要添加引号

#### 字典的常用操作方法

##### 新增与修改

新增与修改使用的语法相同：

```python
# 语法
字典名称[key] = value值

# 定义空字典
person = {}
# 添加数据
person['name'] = 'Tom'
person['gender'] = 'male'
person['age'] = 20
print(person)
# 修改数据
person['name'] = 'Lily'
person['gender'] = 'female'
print(person)
```

##### 删除

删除满足条件的键值对

```python
# 语法
del 字典名称[key]

# 定义一个有数据的字典，'Connor', 'male', 25, 80
student = {'name':'Connor', 'gender':'male', 'age':25, 'weight':80}
# 删除键值对
del student['weight']
print(student)
```

##### 查询

① 查询方法：使用具体的某个key查询数据，如果未找到，则直接报错。

② 字典的相关查询方法

| **编号** | **函数** | **作用**                              |
| -------- | -------- | ------------------------------------- |
| 1        | keys()   | 以类列表返回一个字典所有的键          |
| 2        | values() | 以类列表返回字典中的所有值            |
| 3        | items()  | 以类列表返回可遍历的(键, 值) 元组数据 |

```python
# 定义student = {'name':'Jack', 'age':20, 'address':'广州市天河区'}
student = {'name': 'Jack', 'age': 20, 'address': '广州市天河区'}
# 获取字典中某个元素，打印字典
print(student['address'])
# 遍历字典
for i in student:
    print(i)
# 使用keys()方法获取键值，等价于遍历
for key in student.keys():
    print(key)
# 获取所有的value值，values
for value in student.values():
    print(value)
# 获取所有键值对，items
for item in student.items():
    print(item)
```



#### 列表和字典结合使用

```python
# 开发一个学生管理系统
# 1、定义一个大列表，里面用于保存多个同学的信息
students = []
# 2、定义一个字典，保存同学信息
student = {'name': 'Tom', 'gender': 'male', 'age': 20}
# 3、将字典嵌套在列表中
students.append(student)
print(students)
# 4、多添加几个字典
student1 = {'name': 'Lily', 'gender': 'female', 'age': 21}
student2 = {'name': 'Connor', 'gender': 'female', 'age': 22}
students.append(student1)
students.append(student2)
print(students)
# 5、提示用户输入需要删除的同学信息
del_name = input('请输入需要删除的同学姓名：')
# 6、通过遍历，删除存储该同学信息的字典
for i in students:
    if i['name'] == del_name:
        students.remove(i)
        print('删除成功')
        break
else:
    print('未找到该同学')
print(students)
```

#### 集合

集合是一个==无序==的==不重复==数据容器，使用{}定义

① 集合中的数据没有顺序

② 集合中的数据是不重复的

```python
# 定义空集合只能使用set()
set1 = set()
print(type(set1))
set2 = {}
print(type(set2))

# 定义一个有数据的集合
set3 = {20, 30, 10, 20, 5, 5}
print(set3)  # 去除了重复数据
print(type(set3))

# set()可以把其他类型的数据转换成集合，比如字符串
set4 = set('abcdefg')
print(set4)
print(type(set4))
```

集合中元素的访问：由于集合中的数据没有顺序，所以其没有索引下标，数据的访问有两种方案
① 直接打印
② 使用for循环对其进行遍历操作（只能使用for循环）

```python
set3 = {20, 30, 10, 20, 5, 5}
for i in set3:
    print(i)
```

#### 集合的常用操作方法

##### 添加

add()，向集合中添加数据

```python
# 定义一个空集合
set1 = set()
# 追加数据10,20,30,40,20,10
set1.add(10)
set1.add(20)
set1.add(30)
set1.add(40)
set1.add(20)
set1.add(10)
print(set1)
```

##### 删除

remove（），根据值删除指定的元素

pop（），随机删除集合中的某个元素，删除后，pop（）方法返回被删除的那个元素

```python
# 删除数据20
set1.remove(20)
print(set1)
# 随机删除某个元素
set1.pop()
print(set1)
```

查询

if 元素 in 集合，判断元素是否出现在集合中，出现True，反之，则返回False

```python
# 判断元素是否出现在集合中
if 40 in set1:
    print('exists')
else:
    print('not exists')
```



#### 数据容器的公共方法

常见方法：

| **运算符** | **描述**             | 支持                           |
| ---------- | -------------------- | ------------------------------ |
| +          | 合并                 | 字符串、列表、元组             |
| *          | 复制                 | 字符串、列表、元组             |
| in         | 元素是否存在         | 字符串、列表、元组、字典、集合 |
| len()      | 返回容器中元素的数量 | 字符串、元组、列表             |
| max()      | 返回容器中的最大值   | 列表、元组、集合               |
| min()      | 返回容器中的最小值   | 列表、元组、集合               |

```python
# 合并或拼接
str1 = 'hello '
str2 = 'Python!'
print(str1 + str2)

list1 = [1, 2, 3, 4, 5]
list2 = [6, 7, 8, 9, 10]
print(list1 + list2)

tuple1 = (1, 2, 3, 4)
tuple2 = (5, 6, 7, 8)
print(tuple1 + tuple2)

# 复制
print(str1 * 10)
print(list1 * 10)
print(tuple1 * 10)

# 是否in
str3 = 'hello python! hello bigdata'
if 'bigdata' in str3:
    print('exists')
else:
    print('not exists')

# 求数据容器长度
print(len(str3))
print(len(list1))
print(len(tuple1))

# 手动输入三个数
num1 = int(input('请输入第一个数:'))
num2 = int(input('请输入第二个数:'))
num3 = int(input('请输入第三个数:'))
# 求三个数的最值
list3 = [num1, num2, num3]
max_num = max(list3)
min_num = min(list3)
print(f'max = {max_num},min = {min_num}')
```



#### 数据容器的相互转换

list()，把其他数据类型转换为list列表类型

tuple()，把其他数据类型转换为tuple元组类型

set()，把其他数据类型转换为set集合类型=>去重

```python
# 元组 -> 列表
tuple1 = (1, 2, 3, 4)
list1 = list(tuple1)
print(list1)
# 集合 -> 列表
set1 = {10, 20, 20, 30, 40}  # 去重了
list2 = list(set1)
print(list2)
# 列表 -> 元组
list3 = ['Tom', 'Connor', 'John', 'Jerry']
tuple2 = tuple(list3)
print(tuple2)
# 集合 -> 元组
set2 = {'a', 'b', 'c', 'd'}
tuple3 = tuple(set2)
print(tuple3)
# 列表 -> 集合
list4= [1, 3, 5, 7, 7, 7, 9]
set3 = set(list4)  # 去重
print(set3)
# 元组 -> 集合
tuple4 = ('a', 'b', 'c', 'd', 'a', 'e', 'b')
set4 = set(tuple4)
print(set4)
```

#### 推导式

简化Python代码

推导式comprehensions（又称解析式），是Python的一种独有特性。推导式是可以从一个数据序列构建另一个新的数据序列（一个有规律的列表或控制一个有规律列表）的结构体。 共有三种推导：`列表推导式`、`集合推导式`、`字典推导式`。

```python
# 基本语法：
变量名 = [表达式 for 变量 in 列表]
变量名 = [表达式 for 变量 in 列表 if 条件]

# 使用while循环创建一个0-9的列表
i = 0
list1 = []
while i <= 9:
    list1.append(i)
    i += 1
print(list1)
# 使用for循环创建一个0-9的列表
list2 = []
for i in range(10):
    list2.append(i)
print(list2)
# 使用推导式创建
list3 = [i for i in range(10)]
print(list3)

# 求0-9之间的偶数
list4 = []
for i in range(10):
    if i % 2 == 0:
        list4.append(i)
print(list4)
# 推导式
list5 = [i for i in range(10) if i % 2 == 0]
print(list5)

# 案例2:有一个列表,里面内容为[1, 2, 3, 4, 5],通过Python代码将其转换为[1, 4, 9, 16, 25]
list6 = [1, 2, 3, 4, 5]
list7 = []
for i in list6:
    list7.append(i ** 2)
print(list7)
# 推导式实现
list8 = [i ** 2 for i in list6]
print(list8)
```



### 7、函数

作用：① 实现代码重用；② 模块化编程（面向过程）

语法：

```python
# 函数的定义
def 函数名称([参数]):
    函数体 
    ...
    [return 返回值]

# 函数的调用
函数名(参数)
```

> 注意：函数必须先定义后调用

思考1：如果一个函数如些两个return (如下所示)，程序如何执行？

```python
def return_num():
    return 1
    return 2


result = return_num()
print(result)  # 1
```

答：只执行了第一个return，原因是因为return可以退出当前函数，导致return下方的代码不执行。

思考2：如果一个函数要有多个返回值，该如何书写代码？

答：在Python中，理论上一个函数只能返回一个结果。但是如果我们向让一个函数可以同时返回多个结果，我们可以使用`return 元组`的形式。

```python
def return_num():
    return 1, 2


result = return_num()
print(result)
print(type(result))  # <class 'tuple'>
```

思考3：封装一个函数，参数有两个num1，num2，求两个数的四则运算结果

四则运算：加、减、乘、除

```python
def size(num1, num2):
    jia = num1 + num2
    jian = num1 - num2
    cheng = num1 * num2
    chu = num1 / num2
    return jia, jian, cheng, chu

# 调用size方法
print(size(20, 5))
```

#### 函数的说明文档

思考：如果代码多，我们是不是需要在很多代码中找到这个函数定义的位置才能看到注释？如果想更方便的查看函数的作用怎么办？

答：==函数的说明文档（函数的说明文档也叫函数的文档说明）==

函数说明文档：就相当于函数的说明书，在这个说明书中我们需要标注这个函数的作用、拥有的参数以及最终的返回值！

```python
def func():
    ''' 函数说明文档 '''
    函数体代码
```

如何快速查看函数的说明文档呢？
help（函数名称）
可以基于PyCharm中快捷键 => Ctrl+Q

#### 函数的嵌套

在一个函数中调用了另一个函数

```python
# 定义一个testB函数
def testB():
    print('----- testB start -----')
    print('testB函数体代码...')
    print('----- testB end -----')


# 定义一个testA函数，在其中调用testB
def testA():
    print('----- testA start -----')
    testB()
    print('----- testA end -----')


# 调用testA函数
testA()

```

debug函数需要使用step into

在 PyCharm 中，step over、step into 和 step into my code 是调试器中常用的三个功能，它们的区别如下：

1. Step Over：该功能会执行当前行代码，并停在下一行代码上。如果下一行是一个函数调用，则该函数的所有代码将会一次性执行，但调试器不会进入到这个函数的内部。可以理解为该功能是跳过当前函数，进入下一个函数的功能。
2. Step Into：该功能会进入到当前行代码中的函数或方法内部，并停在函数或方法内部的第一行代码上，即进入函数内部进行调试。如果当前行没有函数或方法调用，则该功能的效果和 Step Over 相同。
3. Step Into My Code：该功能和 Step Into 功能类似，区别在于 Step Into My Code 只会进入你自己编写的函数或方法中，不会进入 Python 标准库或第三方库中的函数或方法中进行调试。

#### 函数使用案例

```python
# 求三个数平均值
def avg_func(num1, num2, num3):
    '''
    该函数用于求三个数的平均值
    :param num1: int，参数1
    :param num2: int，参数2
    :param num3: int，参数3
    :return: 返回三个数的平均值avg
    '''
    avg = (num1 + num2 + num3) / 3
    return avg


num1 = int(input('请输入第1个数：'))
num2 = int(input('请输入第2个数：'))
num3 = int(input('请输入第3个数：'))
result1 = avg_func(num1, num2, num3)
print(result1)


# 编写一个函数,有一个参数str1,输入信息如'1.2.3.4.5',使用函数对其进行处理,要求最终的返回结果为'5-4-3-2-1'
def str_func(str1):
    '''
    将输入字符串先翻转，然后将’.‘替换为’-‘
    :param str1: str，参数1
    :return: 返回处理后字符串
    '''
    str2 = str1[::-1]  # 翻转字符串
    result = str2.replace('.', '-')  # 替换
    return result


result2 = str_func('1.2.3.4.5')
print(result2)


# 生成4位数的验证码
import random
def code_func():
    '''
    用于随机生成4位验证码
    :return: 返回4位的验证码
    '''
    str1 = '23456789abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ'  # 验证码的范围
    code = ''  # 定义空容器存储验证码
    i = 1
    while i <= 4:  # 生成4位，即循环4次
        index = random.randint(0, len(str1) - 1)  # 求出字符串中的随机一个索引
        code += str1[index]  # 按照索引，切片1个字符
        i += 1
    return code


result3 = code_func()
print(f'验证码为：{result3}')

```



#### 变量的作用域

作用域：变量可以使用的区域，全局作用域即函数外面的区域，局部作用域即函数内部的区域。

根据作用域，变量可以分为两类，全局变量和局部变量

全局变量既可以在全局作用域中访问，也可以在局部作用域中访问

局部变量只能在局部作用域中访问

##### global关键字

可实现在局部作用域中对全局变量的修改操作

```python
# 使用global修改全局变量
num = 10
def func():
    global num  # 从该行开始，以后使用的num都是全局变量
    num = 100


func()
print(num)  # 成功修改num
```

> 记住：global关键字只是针对不可变数据类型的变量进行修改操作(数值、字符串、布尔类型、元组类型),可变类型可以不加global关键字.

#### 函数传参

函数中的参数分为两类：形参、实参

==形参：在函数定义时，所编写的参数就称之为形式参数，是局部变量==

==实参：在函数调用时，所传递的参数就称之为实际参数==

```python
def greet(name):  # name一个形参
    # name作用域只在此函数内部有效,因为其是一个局部变量
    return 'hello,' + name


# 定义一个全局变量
name = '老王'
greet(name)  # 函调用时所指定的参数是一个实参,通常是一个全局变量

```

#### 传参方式

① 位置传参

② 关键词传参

```python
# 定义一个函数
def func(name, age, mobile):
    print(name)
    print(age)
    print(mobile)


# ①位置传参,根据函数定义时参数的位置传递参数的值(强调参数的位置,顺序不能颠倒)
func('Tom', 23, '10000')

# ②关键词传参,根据"参数=值方式来实现对参数的传递,优势:不需要考虑位置关系,只要参数名称没错,任何位置都可以
func(name='Jack', mobile='10010', age=19)
```

#### 函数定义时的参数

在python代码中,函数定义时的参数一共有3种类别：

① 普通参数，如def func(name, age,mobile)

② 缺省参数（默认值参数），如def func(name, age, gender='male')

③ 不定长参数，如def func(*args,**kwargs)

#### 不定长参数

不定长参数也叫可变参数。用于不确定调用的时候会传递多少个参数(不传参也可以)的场景。此时，可用==包裹(packing)位置参数==，或者==包裹关键字参数==，来进行参数传递，会显得非常方便。

\*args：不定长位置参数(不定长元组参数)，*args代表固定格式，args代表变量的名称，主要用于接收不定长位置参数

\*\*kwargs：不定长关键词参数（不定长字典参数），\*\*kwargs代表固定格式，kwargs代表变量名称，主要用于接收不定长关键词参数

```python
# 不定长位置参数
def func1(*args):
    print(args)


# 多种方式调用函数
func1()
func1(1)
func1(1, 3, 5)  # 返回元组


# 不定长关键词参数
def func2(**kwargs):
    print(kwargs)


func2()
func2(a=1)
func2(a=1, b=3, c=5)


# 两个一起用
def func3(*args, **kwargs):  # *args必须放在左边，**kwargs必须放在右边
    print(args)
    print(kwargs)


func3(1, 2, 3, a=4, b=5, c=6)  # *args接收位置参数，**kwargs接收关键词参数

```

应用场景：

```python
```

#### 参数混用

函数中，可以把普通参数，缺省参数，不定长参数混合使用，==特别注意：顺序很重要==

```python
# 语法
def func(① 普通参数 ② *args ③ 缺省参数 ④ **kwargs):
    pass

# 四种参数混用
def func(a, b, *args, c=4, **kwargs):
    print(a, b)
    print(args)
    print(c)
    print(kwargs)


func(1, 2, 50, c=100, d=5, e=6)  # 此时传递默认值参数时需要写全
```

#### 引用变量与可变、非可变类型

```python
a = 10

print(id(a))  # 查看a所指向的内存地址
```

第一步：首先在计算机内存中创建一个数值10（占用一块内存空间）

第二步：在栈空间中声明一个变量，如a

第三步：把数值10的内存地址赋予给变量小a，形成所谓的==“引用关系”==



在Python中，我们可以把7种数据类型分为两大类：可变类型 + 非可变类型

① 不可变类型（内存地址一旦固定，其值就不能发生改变）

数值（int整型、float浮点类型）

bool类型（True和False）

字符串类型（str）

元组（tuple 1,2,3）

② 可变类型（内存地址一旦固定，其值是可以发生改变）

列表（list [1, 2, 3]）

字典（dict {key:value})

集合（set {1, 2})

```python
# 定义函数
def func(num2, names2):
    num2 += 10  # 无法在局部作用域修改不可变类型的变量
    names2.append('Connor')  # 可以在局部作用域修改可变类型的变量


# 定义全局变量
num1 = 10
names1 = ['Herry', 'Jerry', 'Tom']
# 调用函数
func(num1, names1)

print(num1, names1)  # 10  ['Herry', 'Jerry', 'Tom', 'Connor']
```



#### 元组拆包

简单来说就是把一个元组中的数据一个一个拆解出来的过程，就称之为叫做拆包操作。

语法

```python
tuple1 = (10, 20, 30)
# 拆包
num1, num2, num3 = tuple1

# 以上代码可以简写为
num1, num2, num3 = (10, 20, 30)
# 还可简写为
num1, num2, num3 = 10, 20, 30
print(num1, num2, num3)

# 案例：实现两个变量的交换
c1 = 'cola'
c2 = 'milk'

c2, c1 = c1, c2
print(c1)
print(c2)

```

### 8、文件操作

步骤：① 打开文件，② 读写文件， ③ 关闭文件

#### open函数打开文件

语法

```python
f = open(name, mode)
# 注：返回的结果是一个file文件对象（后续会学习，只需要记住，后续方法都是f.方法()）
```

name：是要打开的目标文件名的字符串(可以包含文件所在的具体路径)。

mode：设置打开文件的模式(访问模式)：只读r、写入w、追加a等。

> r模式：代表以只读模式打开一个已存在的文件，后续我们对这个文件只能进行读取操作。如果文件不存在，则直接报错。另外，r模式在打开文件时，会将光标放在文件的第一行（开始位置）。

> w模式：代表以只写模式打开一个文件，文件不存在，则自动创建该文件。w模式主要是针对文件写入而定义的模式。但是，要特别注意，w模式在写入时，光标也是置于第一行同时还会清空原有文件内容。

> a模式：代表以追加模式打开一个文件，文件不存在，则自动创建该文件。a模式主要也是针对文件写入而定义模式。但是和w模式有所不同，a模式不会清空文件的原有内容，而是在文件的尾部追加内容。

```python
# 使用python.txt举例
f = open('python.txt', 'w')  # 打开文件
# 写入内容
f.write('Life is short, I study Python!')
# 关闭文件，节省计算机资源
f.close()

```



#### 文件读取

`read(size)方法`：主要用于文本类型或者二进制文件（图片、音频、视频...）数据的读取

size表示要从文件中读取的数据的长度（单位是字符/字节），如果没有传入size，那么就表示读取文件中所有的数据。

```python
# read(size)方法
# r模式，打开文件
f = open('python.txt', 'r', encoding='utf-8')
# 读取文件内容
# content = f.read()  # 读取文件所有内容
content = f.read(1)  # 只读取一个字符
print(content)

# 关闭文件
f.close()

```



`readlines()方法`：主要用于文本类型数据的读取

readlines可以按照行的方式把整个文件中的内容进行一次性读取，并且返回的是一个列表，其中每一行的数据为一个元素。

```python
# readlines方法
f = open('python.txt', 'r', encoding='utf-8')
# 读取文件内容
content = f.readlines()
print(content)
# 关闭文件
f.close()
```

`readline()方法`：一次读取一行内容，每运行一次readline()函数，其就会将文件的指针向下移动一行

```python
# readline方法
f = open('python.txt', 'r', encoding='utf-8')
# 使用循环实现一次执行读取多行
while True:
    content = f.readline()
    if not content:  # 当文件内容读取完后继续读会产生空内容，判断是否为空即可中断循环
        break
    print(content, end='')  # 解决每print一次就会出现一次空行的问题
# 关闭文件
f.close()
```

#### 文件打开模式

| **模式** | **描述**                                                     |
| -------- | ------------------------------------------------------------ |
| r        | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
| rb       | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。 |
| r+       | 打开一个文件用于读写。文件指针将会放在文件的开头。           |
| rb+      | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。 |
| w        | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| wb       | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| w+       | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| wb+      | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| a        | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| ab       | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| a+       | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。 |
| ab+      | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。 |

> 虽然mode文件操作模式很多，但是我们只需要记住3个字符即可。r、w、a

> r+、w+、a+，代加号，功能全，既能读，又能写（区别在于指针到底指向不同）

> rb、wb、ab，代b的字符，代表以二进制的形式对其进行操作，适合读取文本或二进制格式文件，如图片、音频、视频等格式

> rb+、wb+、ab+，代加号，功能全，既能读，又能写（区别在于指针到底指向不同）

#### 文件备份

需求：用户输入当前目录下任意文件名，完成对该文件的备份功能(备份文件名为xx[备份]后缀，例如：(test[备份].txt)。

```python
# 需求：用户输入当前目录下任意文件名，完成对该文件的备份功能(备份文件名为xx[备份]后缀，例如：(test[备份].txt)。
# ①命名变化:test.txt => 备份 => test[备份].txt
# ②内容变化:需要把旧文件中的内容完全拷贝到新文件中
# rfind()方法,从左向右查找,返回这个关键词在最后一次出现的位置
oldname = input('请输入您要备份的文件名称:')
index = oldname.rfind('.')
filename = oldname[:index]
postfix = oldname[index:]
newname = filename + '[备份]' + postfix
# 打开旧文件，创建新文件
old_f = open(oldname, 'rb')
new_f = open(newname, 'wb')
# 读取文件，写入内容
while True:
    content = old_f.read(1024)
    if not content:
        break
    new_f.write(content)

old_f.close()
new_f.close()
```



#### 文件操作

需要使用os模块的相关功能

| **编号** | **函数**                          | **功能**             |
| -------- | --------------------------------- | -------------------- |
| 1        | os.rename(旧文件名称，新文件名称) | 对文件进行重命名操作 |
| 2        | os.remove(要删除文件名称)         | 对文件进行删除操作   |

案例：把Python项目目录下的python.txt文件，更名为linux.txt，休眠20s，刷新后，查看效果，然后对这个文件进行删除操作。

```python
# 案例：把Python项目目录下的python.txt文件，更名为linux.txt，
# 查看效果，然后对这个文件进行删除操作。
import os
if os.path.exists('python.txt'):  # 判断文件是否存在，防止不存在时报错
    os.rename('python.txt', 'linux.txt')
os.remove('linux.txt')
```



#### 文件夹操作

相关方法：

| **编号** | **函数**                 | **功能**                                    |
| -------- | ------------------------ | ------------------------------------------- |
| 1        | os.mkdir(新文件夹名称)   | 创建一个指定名称的文件夹                    |
| 2        | os.getcwd()              | current  work   directory，获取当前目录名称 |
| 3        | os.chdir(切换后目录名称) | change  directory，切换目录                 |
| 4        | os.listdir(目标目录)     | 获取指定目录下的文件信息，返回列表          |
| 5        | os.rmdir(目标目录)       | 用于删除一个指定名称的"空"文件夹            |

案例：准备一个static文件夹以及file1.txt、file2.txt、file3.txt三个文件

① 在程序中，将当前目录切换到static文件夹

② 创建一个新images文件夹以及test文件夹

③ 获取目录下的所有文件

④ 移除test文件夹

```python
import os
os.chdir('static')  # 切换
print(os.getcwd())  # 查看当前目录
if not os.path.exists('images'):  # 判断是否存在
    os.mkdir('images')
if not os.path.exists('test'):
    os.mkdir('test')
print(os.listdir())  # 查看所有文件
os.rmdir('test')

```



#### 路径问题

绝对路径：从盘符开始，一级一级向下移动，不能越级

```python
D:/PycharmProjects/pythonProject/static
```

缺点：不适合迁移



相对路径：以当前正在运行的工作目录作为参考点

① 同级路径，都在同一个文件夹中，兄弟关系，如static目录下有file1.txt和file2.txt，则file1.txt和file2.txt就是同级关系，==同级访问直接使用名称即可或者使用./文件名称==。

② 下一级路径，我们的文件与另外一个文件存在上下级关系，如images文件夹中存在一个avatar文件夹，则images是上级目录，avatar是下级目录。==则我们访问avatar可以通过images/avatar来实现==。

③ 上一级路径，如果我们某些时候，向从当前目录下，跳出到外一层路径，我们可以使用==../==来实现。

#### 递归删除

```python
# 导入shutil模块
import shutil

# 递归删除非空目录
shutil.rmtree('要删除文件夹路径')
```

> 递归删除文件夹的原理：理论上，其在删除过程中，如果文件夹非空，则自动切换到文件夹的内部，然后把其内部的文件，一个一个删除，当所有文件删除完毕后，返回到上一级目录，删除文件夹本身。

### 9、异常

异常并不是错误，两者有所不同。异常往往是由于输入信息异常或者未知的结果导致程序无法执行！

异常演示：

```python
# 除数异常
print(10 / 0)

# 文件读取异常
f = open('python.txt', 'r')
content = f.readlines()
print(content)
```



#### 异常捕获

try...except主要用于捕获代码运行时异常，如果异常发生，则执行except中的代码

语法：

```python
try:
    可能发生错误的代码
except:
    如果出现异常执行的代码
```

案例：

```python
# # 除数异常
# print(10 / 0)
#
# # 文件读取异常
# f = open('python.txt', 'r')
# content = f.readlines()
# print(content)

# 异常捕获案例，输入数字执行除法
num = int(input('请输入数字：'))
try:
    result = 100 / num
    print(result)
except:
    print('出现异常，执行B计划')

```



##### 捕获异常并输出错误信息

无论我们在except后面定义多少个异常类型，实际应用中，也可能会出现无法捕获的未知异常。这个时候，我们考虑使用Exception异常类型捕获可能遇到的所有未知异常，这里用print演示，实际应写入日志中

```python
try:
    可能遇到的错误代码
except Exception as e:
    print(e)
```

案例：

```python
# 输出异常信息
try:
    result = 100 / num
    print(result)
except Exception as e:
    print(f'--日志：{e}--')  # 用print代替日志

```



#### else

当try语句中的代码没有出现异常，则执行else语句中的代码，反之，则不执行

#### finally

finally表示的是无论是否异常都要执行的代码

```python
# 加入else，finally
try:
    f = open('python[备份].txt', 'r', encoding='utf-8')
except:
    f = open('python[备份].txt', 'w', encoding='utf-8')
else:
    content = f.readlines()
    print(content)
finally:
    f.close()

```



### 10、模块与包

Python 模块(Module)，是一个==Python 文件==，以 .py 结尾，包含了 Python 对象定义和Python语句。模块能定义==函数，类和变量==，模块里也能包含可执行的代码。

模块通常可以分为两大类：==内置模块(目前使用的)== 和 ==自定义模块==

import代表导入某个或多个模块中的所有功能，但是有些情况下，我们只希望使用这个模块下的某些方法，而不需要全部导入。这个时候就建议采用from 模块名 import 功能名。使用from导入后，调用函数不需要使用模块名称，直接使用函数名称即可。

```python
import 模块名  # 导入整个模块
from 模块名称 import *  # 导入这个模块中所有函数
from 模块名称 import 函数1, 函数2, 函数3  # 仅导入函数123

```

#### time模块

time.sleep(秒数)：休眠指定秒数

time.time()：获取当前时间

```python
# 循环10000000次，每次循环添加一个元素进列表，求程序运行时间
from time import *  # 直接导入time的所有函数
start = time()  # 直接使用函数名获取当前时间，而不需要time.time()
# 开始循环
list1 = []
for i in range(10000000):
    list1.append(i)

end = time()
execution = end - start  # 计算程序执行时间
print(f'程序执行时间为：{execution}s')
```

#### 自定义模块

在Python中，模块一共可以分为两大类：内置系统模块  和  自定义模块

模块的本质：在Python中，模块的本质就是一个Python的独立文件（后缀名.py），里面可以包含==全局变量、函数以及类==。

> 注：在Python中，每个Python文件都可以作为一个模块，模块的名字就是==文件的名字==。也就是说自定义模块名必须要符合标识符命名规则。

> 特别注意：我们在自定义模块时，模块名称不能为中文，不能以数字开头，另外我们自定义的模块名称不能和系统中自带的模块名称(如os、random)相冲突，否则系统模块的功能将无法使用。比如不能定义一个叫做os.py模块

案例：在Python项目中创建一个自定义文件，如my_module1.py

```python
# 封装一个函数sum_num，实现对两个参数的求和
def sum_num(num1, num2):
    print(num1 + num2)
```

导入自定义模块

```python
# 导入自定义函数
import my_module1
my_module1.sum_num(10, 20)

from my_module1 import sum_num
sum_num(10, 20)
```

在我们编写完自定义模块以后，最好在模块中对代码进行提前测试，以防止有任何异常。

测试需求：

① 要求我们可以直接在模块文件中对代码进行直接测试

② 代码测试完毕后，当导入到其他文件时，测试代码要自动失效



引入一个魔术变量：`__name__`，其保存的内容就是一个==字符串类型==的数据。

==随着运行页面的不同，其返回结果也是不同的：==

① 如果`__name__`是在当前页面运行时，其返回结果为`__main__`

② 如果`__name__`在第三方页面导入运行时，其返回结果为模块名称（文件名称）

基于以上特性，我们可以把`__name__`编写在自定义模块中，其语法如下：

```python
if __name__ == '__main__':
    # 执行测试代码
```

> 以上代码主要出现在自定义模块中，主要用于实现代码测试

```python
def func1():
    return 1


def func2():
    return 2


def func3():
    return 3


if __name__ == '__main__':  # 只有在当前页面运行__name__才会等于__main__
    print(__name__)
    print(func1())
    print(func2())
    print(func3())

```



### 11、学生管理系统开发

#### 最终效果

```
------------------------------------
		学生管理系统	v1.0
【1】添加学生的信息
【2】删除学生的信息
【3】修改学生的信息
【4】查询学生的信息
【5】遍历所有学生的信息
【6】保存数据到文件
【7】退出系统
------------------------------------
```

#### 需求分析

需求：进入系统显示系统功能界面，功能如下：

① 添加学员信息

② 删除学员信息

③ 修改学员信息

④ 查询学员信息(只查询某个学员)

⑤ 遍历所有学员信息

⑥ 退出系统

系统共6个功能，用户根据自己需求选取

#### 功能实现步骤

① 显示功能界面

② 用户输入功能序号

③ 根据用户输入的功能序号，执行不同的功能(函数)

模块化的编程思想是最早期的编程思想，其强调==把一个系统分解为若干个功能（步骤）==，每个功能就是一个模块（函数）。当所有功能开发完毕后，功能整合，则系统就完成了。

#### 开发过程

功能菜单

```python
# 定义menu函数，实现对系统功能界面的输出
def menu():
    print('-' * 40)
    print('            学生管理系统v1.0')
    print('【1】添加学生信息')
    print('【2】删除学生信息')
    print('【3】修改学生信息')
    print('【4】查询学生信息')
    print('【5】显示所有学生信息')
    print('【6】保存数据到文件')
    print('【7】加载数据到系统')
    print('【8】退出系统')
    print('-' * 40)
```

判断函数

```python
# 定义is_digit函数，判断用户是否输入数字
def is_digit(user_str):
    try:
        num = int(user_str)
        return num
    except:
        return

```

添加功能

```python
# 定义add_stu函数，实现添加学生信息
def add_stu():
    while True:
        global students
        name = input('请输入学生姓名：')
        # 判断是否输入的是数字
        while True:
            age_str = input('请输入学生年龄：')
            # 嵌套使用函数is_digit来判断
            age = is_digit(age_str)
            if not age:
                print('【输入错误，请按提示输入正确内容！】')
                continue
            else:
                break
        gender = input('请输入学生性别：')
        # 将信息存入字典和列表
        student = {}
        student['name'] = name
        student['age'] = age
        student['gender'] = gender
        students.append(student)
        user_cmd = input('【输入任意键继续】\n【输入q或者Q退出】\n:')
        # 判断退出或继续
        if user_cmd == 'q' or user_cmd == 'Q':
            break
```

删除功能

```python
# 定义del_stu函数，实现删除学生信息
def del_stu():
    while True:
        del_name = input('请输入所要删除的学生姓名：')
        # 遍历学生列表
        for i in students:
            # 判断学生姓名是否存在
            if i['name'] == del_name:
                students.remove(i)
                print(f'【{del_name}】信息已成功删除！')
                break
        # 遍历完成后，没查询到（没有break）时进行提示
        else:
            print('【很抱歉，查询不到该学生！】')

        user_cmd = input('【输入任意键继续】\n【输入q或者Q退出】\n:')
        # 判断退出或继续
        if user_cmd == 'q' or user_cmd == 'Q':
            break

```

修改功能

```python
# 定义alter_stu函数，实现修改学生信息
def alter_stu():
    while True:
        global students
        alter_name = input('请输入所要修改的学生姓名：')
        for i in students:
            if i['name'] == alter_name:
                # 提示输入修改信息
                name = input('请输入新学生姓名：')
                # 判断是否输入的是数字
                while True:
                    age_str = input('请输入学生年龄：')
                    age = is_digit(age_str)
                    if not age:
                        print('【输入错误，请按提示输入正确内容！】')
                        continue
                    else:
                        break
                gender = input('请输入新学生性别：')
                # 修改students列表内的字典
                i['name'] = name
                i['age'] = age
                i['gender'] = gender
                print(f'【{alter_name}】信息已成功修改！')
                break
        # 遍历完成后，没查询到（没有break）时进行提示
        else:
            print('【很抱歉，查询不到该学生！】')

        user_cmd = input('【输入任意键继续】\n【输入q或者Q退出】\n:')
        # 判断退出或继续
        if user_cmd == 'q' or user_cmd == 'Q':
            break

```

查询功能

```python
# 定义select_stu函数，查询单个学生的信息
def select_stu():
    while True:
        select_name = input('请输入所要查询的学生姓名：')
        for i in students:
            if i['name'] == select_name:
                print(f'姓名：{i["name"]}, 年龄：{i["age"]}, 性别：{i["gender"]}')
                break
        else:
            print('【很抱歉，查询不到该学生！】')

        user_cmd = input('【输入任意键继续】\n【输入q或者Q退出】\n:')
        # 判断退出或继续
        if user_cmd == 'q' or user_cmd == 'Q':
            break

```

遍历所有学生信息

```python
# 定义show_all_stu函数，实现展示所有学生信息
def show_all_stu():
    # 判断students是否为空
    if not students:
        print('【暂无学生信息！】')
    # 非空则输出所有信息
    else:
        for i in students:
            print(f'姓名：{i["name"]}, 年龄：{i["age"]}, 性别：{i["gender"]}')

```

保存数据到文件

```python
# 定义save_data_to_file函数，实现保存数据到txt文件
def save_data_to_file():
    global students
    f = open('students.txt', 'w', encoding='utf-8')
    # 判断列表是否为空
    if not students:
        print('【暂无数据需要保存！】')
    else:
        f.write(str(students))
        print('【数据保存成功！】')
    f.close()

```

加载文件的数据到系统

```python
# 定义load_data_to_sys函数，实现加载文件数据到系统中
def load_data_to_sys():
    global students
    # 判断文件是否存在，防止打开文件报错
    if not os.path.exists('students.txt'):
        print('【文件不存在，请先保存数据至文件！】')
    else:
        f = open('students.txt', 'r', encoding='utf-8')
        content = f.read()
        # 判断文件是否为空
        if not content:
            print('【文件为空，请先保存数据至文件！】')
        else:
            # content为str，需要将其转换为list
            students = eval(content)
            print('【数据加载成功！】')
```

系统的调用

```python
# 加载数据
load_data_to_sys()
# 系统的调用
while True:
    menu()
    user_str = input('请按照提示输入数字：')
    # 判断输入内容是否是数字
    user_num = is_digit(user_str)

    if user_num == 1:
        add_stu()
    elif user_num == 2:
        del_stu()
    elif user_num == 3:
        alter_stu()
    elif user_num == 4:
        select_stu()
    elif user_num == 5:
        show_all_stu()
    elif user_num == 6:
        save_data_to_file()
    elif user_num == 7:
        load_data_to_sys()

    # 退出系统
    elif user_num == 8:
        print('【已成功退出系统，欢迎下次使用！】')
        break

    # 当用户输入错内容时，返回功能提示菜单
    else:
        print('【输入错误，请按提示输入正确内容！】')
        
```



## 二、Python面向对象

### 1、面向对象

面向过程：自顶向下，逐步细化，核心是函数

面向对象：通俗说，就是在编程的时候尽可能的去模拟现实世界。所谓的模拟现实世界，就是使计算机的编程语言在解决相关业务逻辑的时候，与真实的业务逻辑的发生保持一致，需要使任何一个动作的发生都存在一个支配给该动作的一个实体（主体），因为在现实世界中，任何一个功能的实现都可以看做是一个一个的实体在发挥其各自的“功能”（能力）并在内部进行协调有序的调用过程！

面向对象3步走：①分析动作由哪些实体（对象）发出；②定义这些实体，为其增加相应的功能和属性；③让实体执行相应的功能或动作



面向对象与面向过程的区别：

①都可以实现代码重用和模块化编程，面向对象的模块化更深，数据也更封闭和安全

②面向对象的思维方式更加贴近现实生活，更容易解决大型的复杂的业务逻辑

③从前期开发的角度来看，面向对象比面向过程要更复杂，但是从维护和扩展的角度来看，面向对象要远比面向过程简单！

④面向过程的代码执行效率比面向对象高

#### 面向对象的各个概念

对象：object，对象的属性对应变量，对象的功能或动作对应函数和方法，在Python中使用类（class）开生产对象，用类来规定对象的属性和方法

类：类本来就是对现实世界的一种模拟，在现实生活中，任何一个实体都有一个类别，==类就是具有相同或相似属性和动作的一组实体的集合！==

类名：为了和方法名、函数相区分，类名首字母一般大写（大驼峰）

object：所有类的基类

```python
经典类：  # 现在用得很少，python2.0
class 类名:
    代码
    ......
    
    
新式类：  # 主要用该方式，python3.0
class 类名(object):
    代码
    # 属性 => 变量
    # 方法 => 函数
    ......
    
# 实例化类，即获取对象，产生的对象自动拥有类中所有公共属性和公共方法
对象名称 = 类名()

# 调用对象
对象名称.属性
对象名称.方法()
```

#### 类的创建和实例化

案例：定义一个Person类，方法有eat和run，实例化类

```python
# 案例：定义一个Person类，方法有eat和run
class Person(object):
    # 属性
    # 方法
    def eat(self):
        print('i can eat food')

    def run(self):
        print('i can run')
        
# 实例化和调用
p1 = Person()
p1.eat()
p1.Sleep()
p1.run()

p2 = Person()
p2.eat()
p2.Sleep()
p2.run()

# 打印对象可查看内存地址
print(p1)
print(p2)
```

> 类是一个抽象概念，在定义时，其并不会真正的占用计算机的内存空间。但是对象是一个具体的事务，所以其要占用计算机的内存空间。

#### 对象参数self

self也是Python内置的关键字之一，其指向了==类实例对象本身==。

```python
# 1、定义一个类
class Person():
    # 定义一个方法
    def speak(self):
        print(self)


# 2、类的实例化（生成对象）
p1 = Person()

print(p1)
p1.speak()

p2 = Person()
print(p2)
p2.speak()
# print之后p1和self的结果相同，p2和self的结果相同，即证明self指向了实例对象本身

```

一句话总结：类中的self<就是谁实例化了对象，其就指向谁。



#### 添加和获取对象属性

属性即特征，对象属性可以在类的外部和内部添加

```python
# 外部添加
对象名称.属性 = 属性值

# 内部添加


# 外部访问属性
print(对象名称.属性)

# 内部访问属性
class 类名(object):
    
    def print_info(self):
        print(f'属性名:{self.属性}'')
```

举例：

```python
class Person(object):
    # 属性
    # 方法
    def eat(self):
        print('i can eat food')

    def run(self):
        print('i can run')

    def sleep(self):
        print('i can sleep all day')

    # 在类内部获取属性
    def print_info(self):
        print(f'姓名：{self.name}')
        print(f'年龄：{self.age}')


p1 = Person()
# 在类外部添加属性
p1.name = 'Tom'
p1.age = 20

# 在类外部访问属性
print(p1.name)
print(p1.age)

# 访问属性
p1.print_info()

```



#### 魔术方法

直接在在类的内部描述未来对象所拥有的一些公共属性，以减少重复添加属性的冗余代码

`__name__, __file__`都是魔术变量，`__xxx__()`的函数叫做魔法方法

##### `__init__()`初始化方法

触发条件：实例化对象， 每实例化一次就触发一次

作用：实例化对象时，连带其中的参数，会一并传给``__init__``函数自动并执行它。`__init__()`函数的参数列表会在开头多出一项，它永远指代新建的那个实例对象，Python语法要求这个参数必须要有，名称为self。

```python
# __init__ 初始化方法，在其他编程语言中也称为构造函数
class Person(object):
    # 未来对象所拥有的公共属性
    def __init__(self, name, age, gender):
        self.name = name
        self.age = age
        self.gender = gender

    # 公共方法
    def eat(self):
        print('i can eat food')

    def run(self):
        print('i can run')

    def sleep(self):
        print('i can sleep all day')


# 实例化+传参
p1 = Person('Tom', 23, 'male')
print(p1.name)
print(p1.age)
print(p1.gender)

p2 = Person('Lily', 20, 'female')
print(p2.name)
print(p2.age)
print(p2.gender)

```



##### `__str__()`方法

触发条件：使用print打印

作用：需要打印输出某个对象的信息

```python
# 需求：定义一个汽车类，类实例化对象必须要拥有哪些属性？branc品牌、model型号、color颜色
# 当我们打印这个汽车类对象时，要求输出这辆车的相关信息
class Car(object):
    # 公共属性
    def __init__(self, brand, model, color):
        self.brand = brand
        self.model = model
        self.color = color

    # 公共方法__str__
    # 当对象被打印时,不会弹出对象所指向的内存地址,而是返回__str()__方法中的相关信息
    # 只能用return返回不能使用print，返回的数据必须是str类型
    def __str__(self):
        return f'brand:{self.brand}, model:{self.model}, color:{self.color}'


# 实例化
bmw = Car('BMW', '320', 'black')
print(bmw)

benz = Car('Benz', 'G', 'white')
print(benz)

```



##### `__del__()`删除方法

触发条件：当对象被删除时，自动触发；①手动del对象②当程序结束时，内存开始清理对象

作用：删除对象，项目清理或项目收尾；比如关闭文件，关闭数据库连接

```python
class Person(object):
    # 未来对象所拥有的公共属性，self不需要传参
    def __init__(self, name, age, gender):
        self.name = name
        self.age = age
        self.gender = gender

    # 公共方法
    def __del__(self):
        print('当del对象时，此魔术方法会自动触发')


# 函数执行结束自动触发__del__
p1 = Person('Tom', 23, 'male')
# 手工del对象触发
p2 = Person('Lily', 20, 'female')
del p2

```



#### 综合案例

案例1：

```python
# 案例1：定义学生信息类，包含姓名、成绩属性，定义成绩打印方法
# 90分及以上显示优秀，80分及以上显示良好，70分及以上显示中等，60分及以上显示合格，60分以下显示不及格
class StuInfo(object):
    # 属性
    # 定义学生的私有属性
    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    # 方法
    # 定义学生分数等级的划分方法
    def grade(self):
        if self.__score >= 90:
            print(f'姓名：{self.__name} 分数：{self.__score} 等级：优秀')
        elif self.__score >= 80:
            print(f'姓名：{self.__name} 分数：{self.__score} 等级：良好')
        elif self.__score >= 70:
            print(f'姓名：{self.__name} 分数：{self.__score} 等级：中等')
        elif self.__score >= 60:
            print(f'姓名：{self.__name} 分数：{self.__score} 等级：合格')
        else:
            print(f'姓名：{self.__name} 分数：{self.__score} 等级：不合格')


# 实例化对象
stu1 = StuInfo('Tom', 90)
stu1.grade()

stu2 = StuInfo('Lily', 80)
stu2.grade()

```

记住：在实际工作中，为了保证数据的安全性，一般不建议在类外部直接调用自身属性，如果想调用自身属性都是通过对应的方法实现的！



案例2：

```python
# 案例2：lihua体重75.0公斤，lihua每次跑步会减掉0.10公斤，lihua每次吃东西体重增加0.20公斤。
# 输出lihua信息
class Person(object):
    # 属性
    def __init__(self, name, weight):
        self.__name = name
        self.__weight = weight

    # 方法
    # 使用__str__输出信息
    def __str__(self):
        return f'姓名：{self.__name}，体重：{self.__weight:.2f}'

    # 跑步减重，限制体重的位数
    def run(self):
        self.__weight -= 0.10

    # 进食增重
    def eat(self):
        self.__weight += 0.20


# 实例化对象
Lihua = Person('Lihua', 75)
print(Lihua)

# 执行方法
Lihua.run()
print(Lihua)

Lihua.eat()
print(Lihua)

```



#### 面向对象的三大特性

封装性、继承性、多态性

封装的含义：① 将现实世界中的实体的属性和作用写到类里的操作即为封装；② 可以为属性和方法添加为私有权限

私有（属性、方法）无法在类的外部访问，不能被继承

设置私有属性和私有方法的方式非常简单：在属性名和方法名 前面 加上两个下划线 `__` 即可。

在实际工作中，理论上所有的属性都应该封装为私有形式，保证数据的安全！

```python
class Girl(object):
    # 定义私有属性
    def __init__(self, name):
        self.__name = name
        self.__age = 18

    # 在类的内部定义函数（接口）来访问私有属性
    # 接口
    def getName(self):
        return self.__name

    # 接口
    def getAge(self):
        return self.__age


# 实例化
p1 = Girl('Lily')
# print(p1.name)  # 直接访问私有属性会报错
# print(p1.age)

# 通过接口访问私有属性
print(p1.getAge())
print(p1.getName())

```

### 2、面向对象高级

#### 封装性

定义私有属性：加双下划线`__`

私有属性作用：保护数据；过滤异常数据。

私有属性的接口：通常使用get_xxx接口访问属性，使用set_xxx接口修改属性

访问/修改：1、需要验证用户是否具有查看/修改属性的权限，2、如果有，则可以返回/修改私有属性；如果没有权限，则直接禁止访问/修改

在修改属性时，还可以添加判断来过滤异常异常数据

```python
# 定义Staff类，定义私有属性salary
# 添加访问和设置接口
# 过滤salary异常数据
class Staff(object):
    # 属性
    def __init__(self, name):
        self.name = name
        self.__salary = 10000

    # 访问接口
    def get_salary(self):
        return self.__salary

    # 修改接口
    def set_salary(self, salary):
        # 判断输入数据是否合法，即过滤异常数据
        if not isinstance(salary, int):  # isinstance：判断salary是否是int类型
            print('数据类型不正确')
            return  # 不是int类型就结束接口的使用
        elif salary <= 0:  # 检查数据合理性
            print('数据范围不合理')
            return
        # 数据合理就能正常修改
        self.__salary = salary
        return self.__salary

p1 = Staff('Tom')
print(p1.get_salary())
p1.set_salary(0)
p1.set_salary('aa')
print(p1.set_salary(100000))

```



定义私有方法：加双下划线

作用：简化程序复杂度

```python
# 模拟使用ATM取款
# 银行 => ATM取款 => ①插卡②用户验证③输入取款金额④取款⑤打印账单
class ATM1(object):
    def __card(self):
        print('插卡')

    def __id_verify(self):
        print('用户验证')

    def __input(self):
        print('输入取款金额')

    def __draw_money(self):
        print('取款')

    def __bill(self):
        print('打印账单')

    # 添加公共接口，实现取款操作
    def withdraw(self):
        self.__card()
        self.__id_verify()
        self.__input()
        self.__draw_money()
        self.__bill()


p1 = ATM1()
# 不使用私有方法时，完整取款流程需要调用5个方法
# p1.card()
# p1.id_verify()
# p1.input()
# p1.draw_money()
# p1.bill()
# ======================================================
# 使用私有方法简化程序
p1.withdraw()

```

#### 继承性

在Python中，所有类默认继承object类，object类是顶级类或基类；其他子类叫做派生类。

```python
# 父类B
class B(object):
    pass

# 子类A
class A(B):
    pass
```

子类可以继承父类的所有公共属性和公共方法

继承：一个类从另一个已有的类获得其成员的相关特性，就叫作继承！

派生：从一个已有的类产生一个新的类，称为派生！

很显然，继承和派生其实就是从不同的方向来描述的相同的概念而已，本质上是一样的！



父类：也叫作基类，就是指已有被继承的类！

子类：也叫作派生类或扩展类



扩展：在子类中增加一些自己特有的特性，就叫作扩展，没有扩展，继承也就没有意义了！



多继承：一个类同时继承了多个父类， （C++、Python等语言都支持多继承）

##### 单继承

单继承：一个类只能继承自一个其他的类，不能继承多个类，单继承也是大多数面向对象语言的特性！

多层继承也是单继承的一种延伸，简单来说：A=>B=>C，所以A自动继承了C中的所有公共属性和公共方法

```python
# 定义Person类，具有公共方法：run
# 定义adult子类，继承Person
# 定义worker子类，继承adult
class Person(object):
    # 公共属性
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # 公共方法
    def run(self):
        print('i can run！')


class Adult(Person):
    # 属性
    # 扩展方法
    def work(self):
        print('i can work!')


class Worker(Adult):
    # 扩展方法
    def relax(self):
        print('i want to relax!')


# 实例化，p1能使用Person和Adult的所有公共属性和方法
p1 = Adult('Tom', 19)
print(p1.name)
print(p1.age)
p1.run()
p1.work()

# 实例化，p2能使用所有父类和子类的方法
p2 = Worker('John', 22)
print(p2.name)
print(p2.age)
p2.run()
p2.work()
p2.relax()

```

##### 多继承

多继承就是允许一个类同时继承自多个类的特性。

```python
class C(object):
    pass
class B(object):
    pass

class A(B, C):
    pass
```

案例：

```python
# 定义一个Laptop类
# 定义一个MobilePhone
# 定义一个Pad类，继承上两类的方法
class Laptop(object):
    def func1(self):
        print('I have strong performance!')


class MobilePhone(object):
    def func2(self):
        print('I have portability')


class Pad(Laptop, MobilePhone):
    pass


ipad = Pad()
ipad.func1()
ipad.func2()

```

##### MRO属性/方法

```PYTHON
# 语法
类名.__mro__
类名.mro()
# 需要print
```

继承顺序是：从左到右，依次继承

##### 子类扩展

扩展：在子类中增加自身特有的特性，可重写方法、特性等

重写（覆盖）：当父类方法与子类方法相同时，在子类中重新定义该方法的操作，叫做重写

```python
# 定义Animal类，eat、call方法
# 定义Cat、Dog类
class Animal(object):
    def eat(self):
        print('I can eat')

    def call(self):
        print('I can bark')


class Cat(Animal):
    # 重写父类方法
    def call(self):
        print('meow meow meow')


cat = Cat()
cat.eat()  # 没有重写方法，使用的是父类方法
cat.call()  # 调用父类方法时，使用的是重写后的方法

```

##### super()强制调用方法

当子类中重写父类方法后，依然需要调用父类方法时，就可以使用super

```python
# 语法
super().属性
super().方法()
```

案例：

```python
# 定义Car类，包含初始化属性和run方法
# 定义GasolineCar，重写run方法
# 定义ElectricCar，重写属性和方法
class Car(object):
    # 公共属性
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

    # 公共方法
    def run(self):
        print('Cars can run')


class GasolineCar(Car):
    # 自动继承父类的公共属性
    # 重写方法
    def run(self):
        # 强制继承父类的方法
        super().run()
        print('Cars run with gasoline')


class ElectricCar(Car):
    # 重写父类中的属性
    def __init__(self, brand, color, battery):
        # 强制继承父类中的brand、color属性，只重写battery属性
        super().__init__(brand, color)
        self.battery = battery

    # 重写方法
    def run(self):
        print('Cars run with electricity')


benz = GasolineCar('Benz', 'black')
benz.run()

tesla = ElectricCar('Tesla', 'green', 'Li-battery')
tesla.run()
print(tesla.brand)
print(tesla.color)
print(tesla.battery)

```



#### 多态

定义：多态是一种使用对象的方式，子类重写父类方法，调用不同子类对象的相同父类方法，可以产生不同的执行结果。

==不同对象 => 使用相同方法 => 产生不同的执行结果。==

① 多态依赖继承（不是必须的）

② 子类方法必须要重写父类方法

```python
# 定义Fruit类
class Fruit(object):
    # 公共方法
    def juice(self):
        pass


# 定义子类，重写公共方法
class Apple(Fruit):
    def juice(self):
        print('i like apple juice')


class Orange(Fruit):
    def juice(self):
        print('i like orange juice')


class Watermelon(Fruit):
    def juice(self):
        print('i like watermelon juice')


# 定义一个公共接口service
def service(obj):
    # obj要求是一个实例化对象，可以传入苹果对象/橘子对象
    obj.juice()


# 实例化对象
apple = Apple()
orange = Orange()
# 传入对象
service(apple)
service(orange)
service(Watermelon())  # 或者不实例化对象，直接传入类

```

#### 其他特性

##### 类属性

Python中，属性可以分为① ==对象属性(实例属性或成员属性)== ② ==类属性==。

对象属性：由这个类产生的对象所拥有的属性。

类属性：类对象中定义的属性，它被该类的所有实例对象所共有。通常用来记录 与这类相关的特征，类属性不会用于记录 具体对象的特征。

```python
# 需求：统计这个类生成了多少个对象
# 定义Person类
class Person(object):
    # 定义类属性：计数器，统计对象创建个数
    count = 0
    # 初始化对象属性
    def __init__(self, name, age):
        self.name = name
        self.age = age
        # 对计数器进行累加
        Person.count += 1

p1 = Person('Tom', 23)
P2 = Person('Lily', 20)
# 可以在类的外部直接操作类属性，但不推荐，建议使用类方法
print(f'一共创建了{Person.count}个对象')

```

##### 类方法

类方法：类属性与对象属性一样，都强调封装特性，不建议直接在类的外部直接对类属性进行操作。如果想在类的外部获取类属性的信息，必须使用类方法来实现。

```python
# 语法
class 类名称():
    类属性 = 属性值
    
    @classmethod  # 装饰器，将以下方法装饰成类方法
    def 类方法(cls):  # cls代表类本身
        
# 调用类方法
类名称.类方法()
```

案例：统计tool工具类生成的对象数量

```python
# 案例：统计tool工具类生成的对象数量
class Tool(object):
    # 定义类属性
    count = 0

    # 定义对象属性
    def __init__(self, name):
        self.name = name
        # 计数器累加
        Tool.count += 1

    # 定义类方法（接口）
    @classmethod  # 装饰类方法
    def get_count(cls):
        return f'已实例化对象：{Tool.count}'


t1 = Tool('hammer')
t2 = Tool('axe')
t3 = Tool('nail')
# 调用类方法
print(Tool.get_count())

```

##### 静态方法

在开发时，如果需要在类中封装一个方法，这个方法：  

==① 既 不需要访问实例属性或者调用实例方法==

==② 也不需要访问类属性或者调用类方法==

这个时候，可以把这个方法封装成一个静态方法

```python
# 语法
class 类名称():
    @staticmethod
    def 静态方法():  # 静态方法没有参数
        
# 调用静态方法
类名称.静态方法()
对象名称.静态方法()
```

举例：

```python
# 学生管理系统中的菜单功能
# 菜单功能是独立的
# 不需要调用其他方法或访问属性
class StudentsManager(object):
    # 定义菜单功能，静态方法
    @staticmethod
    def menu():
        print('-' * 40)
        print('            学生管理系统v1.1')
        print('【1】添加学生信息')
        print('【2】删除学生信息')
        print('【3】修改学生信息')
        print('【4】查询学生信息')
        print('【5】显示所有学生信息')
        print('【6】保存数据到文件')
        print('【7】加载数据到系统')
        print('【8】退出系统')
        print('-' * 40)


# 直接调用
StudentsManager.menu()
# 实例化后再调用
p1 = StudentsManager()
p1.menu()

```

