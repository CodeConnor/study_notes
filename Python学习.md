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

## 1、Python基础

创始人：吉多·范罗苏姆(Guido van Rossum)，龟叔

### Python解释器、Pycharm

- Python解释器

作用：运行Python语言，.py文件 -> Python解析器 -> 机器语言

CPython，C语言开发的解释器（官方），应用最广泛

JPython，运行在Java平台的解释器，直接把Python代码编译成Java字节码执行，极大提升了执行效率，但是增加了编译时间。

- Pycharm

一种Python IDE（集成开发工具），Python开发工具。

### 变量、注释

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

② 大驼峰：即每个单词首字母都大写，例如：MyName；Python中用于类名

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



### Bug和Debug

- bug

  三步法：

  ① 查错误文件

  ② 查行号

  ③ 查看错误描述

  

- Debug调试工具：逐步执行代码，可查看与分析Python解析器是如何解析Python代码的

  使用：①打断点；②启动Debug调试

  对于简单的代码我们可以直接在第一行添加一个断点；对于复杂的程序，有逻辑关键字如if/while/for等等，断点必须添加到关键字的前面



### print输出

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

### input输入

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

### 运算符

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



### if选择结构

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



### 循环结构

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



### 数据容器

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
```

##### 字符串判断

isdigit()：判断一个字符串是否全部由纯数字组成，纯数字返回True，反之返回False

```python
```

