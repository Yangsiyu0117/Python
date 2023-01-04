# Python基础笔记

[TOC]

## 变量

### 什么是变量？

变：现实世界中的状态是会发生改变的

量：记录现实世界中的状态，让计算机能够像人一样去识别世间万物

### 定义变量

```python
name = 'nick'
age = 19
gender = 'male'
height = 180
weight = 140
```

### 变量的组成

1. 变量名：变量名用来引用变量值，但凡需要用变量值，都需要通过变量名。
2. 赋值符号：赋值
3. 变量值：存放数据，用来记录现实世界中的某种状态。

### 变量的命名规范

1. 变量的命名应该能反映变量值所描述的状态，切记不可用中文
2. 变量名必须用字母数字下划线组合，并且变量名的第一个字符不能是数字。
3. 关键字不能声明为变量名

### 变量的两种风格

1. 驼峰体

```python
AgeOfNick = 19
print(AgeOfNick)
```

```python
19
```

1. 下划线（推荐）

```python
age_of_nick = 19
print(age_of_nick)
```

```python
19
```

- ## 常量

变量是变化的量，常量则是不变的量。python中没有使用语法强制定义常量，也就是说，python中定义常量本质上就是变量。如果非要定义常量，变量名必须全大写。

```python
AGE_OF_NICK = 19
print(AGE_OF_NICK)
```

```python
19
```

```python
AGE_OF_NICK = AGE_OF_NICK + 1
print(AGE_OF_NICK)
```

```python
20
```

如果是常量，那就没必要更改，所以python就只制定了一个规范，而没指定常量的语法，**因此常量也是可以修改的，但不建议。**

- ## Python变量内存管理

1. 变量存储在内存中
2. Python垃圾回收机制（如果变量新取值，旧值贼会被释放掉）
3. 引用计数

```python
x = 10  # 10引用计数加1为1
y = x  # 10引用计数加1为2
x = 11  # 10引用计数减1为1；11引用计数加1为1
del y  # 10引用计数减1为0，触发python垃圾回收机制，python清理10的内存占用

# 测试
>>> x = 10
>>> y = x
>>> x = 11
>>> y
10
>>> del y
>>> y
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'y' is not defined
>>> x
11
```

4. 小整数池

对于上一节讲的引用计数，需要注意的是：Python实现int的时候有个小整数池。为了避免因创建相同的值而重复申请内存空间所带来的效率问题， Python解释器会在启动时创建出小整数池，**范围是[-5,256]**，该范围内的小整数对象是全局解释器范围内被重复使用，永远不会被垃圾回收机制回收。

在pycharm中运行python程序时，pycharm出于对性能的考虑，会扩大小整数池的范围，其他的字符串等不可变类型也都包含在内一便采用相同的方式处理了，我们只需要记住这是一种优化机制，至于范围到底多大，无需细究。

- ## 小知识点

python内置函数：**id()**

通过这个函数可以获取某一个变量所在的内存地址

```python
>>> year = 2021
>>> print(id(year))
140201597743824
>>>
```

python内置sys模板中的函数：**getrefcount()**

获取某一个变量的引用计数（getrefcount输出值默认从3开始）

```python
>>> import sys
>>> year = 2021
>>> print(sys.getrefcount(year))
2
>>> toyear = year
>>> print(sys.getrefcount(year))
3
>>> yesyear = year
>>> print(sys.getrefcount(year))
4
>>> del yesyear
>>> print(sys.getrefcount(year))
3

>>> print(sys.getrefcount(111111))
3
>>> num = 111111
>>> print(sys.getrefcount(111111))
3
>>> num_1 = 111111
>>> print(sys.getrefcount(111111))
3
>>> num_2 = num_1
>>> print(sys.getrefcount(111111))
3
>>> print(sys.getrefcount(num_1))
3
>>> print(sys.getrefcount(num))
2
```

在Python中让引用计数增加共有三种方法：

1. 变量被创建，变量值引用计数加1
2. 变量被引用，变量值引用计数加1
3. 变量作为参数传入到一个函数，变量值引用计数加2

- ## 变量的三个特征

1. 打印

```python
>>> x = 10
>>> print(x)	# 获取变量的变量值
10
```

2. 判断变量值是否相等

```python
>>> name = 'ysy'
>>> name2 = 'yqq'
>>> print(name == name2)
False
```

3. 判断变量id是否相等

```python
>>> x = 11
>>> y = x
>>> z = 11
>>> print(x == y)
True
>>> print(x is y)
True
>>> print(x is z)	# True，整数池的原因
True
```

```python
>>> x = 257
>>> z = 257
>>> print(x is z)
False
```

## 基本数据类型

### 1.整形

> 作用：记录年龄、个数、年份、等级等
>
> 定义：

```python
>>> age = 18
```

> 使用：

```python
>>> age = 18
>>> res = age * 10
>>> print(res)
180
>>> print(age > 10)
True
```

### 2.浮点（float）

> 作用：记录升高、体重、薪资等

> 定义：

```python
>>> salary = 3.1
>>> print (type(salary))
<class 'float'>
```

> 使用：

```python
>>> print(salary + 1)
4.1
>>> print(3.1 + 1)
4.1
>>> print(3.1 > 1)
True
```

整型+浮点型（数字类型）

> 额外知识点（复数），用于科学计算、人工智能

```python
>>> x = 1 + 2j
>>> x.real
1.0
>>> x.imag
2.0
```

### 3.字符串（str）

> 作用：记录名字、性别、国籍等描述性质的状态

> 定义：引号（'',"",'''''',""""""）内包含一串字符

```python
>>> s1 = 'abc'
>>> print(type(s1))
<class 'str'>
```

> 区别：

```python
>>> s2 = """
... aaa
... bbb
... ccc
... """
>>> print(type(s2))
<class 'str'>
```

> 注意1：注意引号的嵌套

```python
>>> print('my name is "xiaoyunwei"')
my name is "xiaoyunwei"
```

> 注意2：字符串内部是可以有转义符

```python
>>> print('my name is \nxiaoyunwei')
my name is
xiaoyunwei

>>> print('my name i\ts \nxiaoyunwei')
my name i       s
xiaoyunwei

\r\n 换行（python、linux默认用/n）

>>> print('aaa',end='\n')
aaa

>>> print('aaa',end='')
aaa>>> print('bbb',end='')
bbb>>>
```

> 注意3：原生字符串

```python
>>> file_path = "C:\aaa\new.txt"
>>> print(file_path)
C:aa
ew.txt

# 解决方案1
>>> file_path = "C:\\aaa\\new.txt"
>>> print(file_path)
C:\aaa\new.txt
# 解决方案2
>>> file_path = r"C:\aaa\new.txt"
>>> print(file_path)
C:\aaa\new.txt
```

> 使用：

```python
>>> name = "xiaoyunwei"
>>> print(name)
xiaoyunwei

#字符串相加（对空间的占用比较大，字符串的拼接最好不要用）
>>> print("abc"+"efg")
abcefg
# 字符创相乘
>>> print("abc" * 10)
abcabcabcabcabcabcabcabcabcabc
>>> print("=" * 50 + "Hello world")
==================================================Hello world
>>> print("Hello World")
Hello World
>>> print("=" * 50)
==================================================
```

额外知识点：整型、浮点型、字符串存的都是一个值

### 4.list（列表）

list==>索引对应值，索引反应的是位置/顺序（有序）

>  作用：按照顺序把多个值放在一起

> 定义：在[]内用逗号分隔开多个任意类型的值

```python
					0    1     2         3
>>> l1 = [111,3.3,"aaa",[222,333]]
```

> 使用：

```python
>>> print(l1)
[111, 3.3, 'aaa', [222, 333]]

>>> print(l1[0])
111
>>> print(l1[-1])
[222, 333]
>>> print(l1[100])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range			#索引超出范围，报错

>>> print(l1[3][1])			# 嵌套取值
333

>>> l2 = ["张三","李四","王五"]
>>> print(l2[0])
张三
>>> print(l2[1])
李四
>>> print(l2[2])
王五

>>> students_info = [
... ['student1',18,["read","music"]],
... ['student2',19,["play","music"]],
... ['student3',20,["movie","music"]]
... ]
>>> print(students_info[1][2][1])			#第二个学生的第二个爱好
music
```

### 6.字典（dict）

key对应值，称之为map类型/映射类型

> 作用：按照key:value的方式吧多个value放在一起，
>
> ​		  其中value通常是任意类型
>
> ​		  而key通常是字符串类型，用来描述value的属性

> 定义：{}内用逗号分隔开多个key:value的值

```python
>>> d = {"k1":111,"k2":3.1,"k3":"aaa","k4":[222,333],"k5":{"kk":444}}

```

> 使用：

```python
>>> print(d["k1"])
111
>>> print(d["k4"][1])
333
>>> print(d["k5"]["kk"])
444

>>> info = {"name":"xiaoyunwei","age":22,"gender":"woman","level":10}
>>> print(info["level"])
10

>>> students_info = [
... {"name":"xiaoyunwei","age":22,"gender":"woman"},
... {"name":"liangliang","age":23,"gender":"male"},
... {"name":"hanhan","age":24,"gender":"male"},
... ]
>>> print(students_info[1]["name"])			#第二个学生的姓名
liangliang
```

### 7.布尔类型（bool）

值：True/False

> 作用：主要用于判断

> 定义：如何得到布尔值

```python
# 显示的布尔值
# 1、直接定义
x = True
y = False
# 2、通过比较运算
print(10 > 3)
print(10 >= 3)
print("xiaoyunwei" == "xiaoyunwei")

# 隐式的布尔值
# 所有类型的变量值都具有隐式的布尔值，前提是它们得放到条件中
# 其中0，None、空（它们三者隐式的布尔值为False，其他的都为True）
if True:
    print('hello')

if 10 > 3:
    print('hello')
    
if 0:
    print('hello')

if None:
    print('hello')
```

## 输入输出

```python
# 1、python3中的input会吧用户输入的任意内容都存成str类型
print("start....")
name = input("请输入用户名：") # "123"
print(name == "xiaoyunwei")
print('end...',name,type(name))

start....
请输入用户名：xiaoyunwei
True
end... xiaoyunwei <class 'str'>

#python2
name = raw_input("your name：")
# python2中的input必须输入一个明确的类型，你输入什么类型，存的就是什么类型

#python：解释性、强类型（数据类型不允许你随便进行修改，除非这门语言给你放水）
#shell：弱类型，解释器
#静态类型语言（go,在运行之前就确定）、动态类型语言（python。在运行那一刻才确定）

# 2、print
# 格式化输出%s(输入字符创)，%d(整型)，%f(浮点型)
res = "my name is %s my age is %s" % ("xiaoyunwei","18")
print(res)
my name is xiaoyunwei my age is 18
```

## 基本运算符

### 算数运算符

```python
print(10 / 3)
print(10 // 3)
print(10 % 3)
3.3333333333333335
3
1
```

### 比较运算

```python
#关于相等性比较所有类型都可以混着用
print("xiaoyunwei" == 10)
print("xiaoyunwei" != 10)
print([111,222] == [222,111])
False
True
False

#> >= < <=主要用于数字类型
#了解：比长度
print("abcdef" > "abz")
print(len("abcd") > len("abz"))
False
True
# 列表比大小，主要是用于同一种类型
l1 = ['abc',123]
l2 = [123,'abc']
print(l1 > l2)
Traceback (most recent call last):
  File "/mnt/c/Users/86155/Desktop/ORM/输入输出.py", line 28, in <module>
    print(l1 > l2)
TypeError: '>' not supported between instances of 'str' and 'int'			#报错
    
l1 = ['abc','zzz']
l2 = ['abc','abc']
print(l1 > l2)
True
```

### 赋值运算符

```python
# 增量赋值
age = 18
#age += 1   # age = age +1 
age = age + 1
print(age)
#输出
19

x = 10
x %= 3 # x = x %3 
print(x)
#输出
1  	# 余数

# 链式赋值
x = y = z =10   	#这就是链式赋值
x = 10
y = x
z = y
print(id(x))
print(id(y))
print(id(z))
#输出
94102804542688
94102804542688
94102804542688

# 交叉赋值
x = 10
y = 20
x,y = y,x

# 解压赋值
salaries = [11,22,33,44,55,66]
mon0 = salaries[0]
mon1 = salaries[1]
mon2 = salaries[2]
mon3 = salaries[3]
mon4 = salaries[4]
mon5 = salaries[5]
#强调：变量名的个数与值应该一一对应
# mon0,mon1,mon2,mon3,mon4,mon5=salaries
print(mon0,mon1,mon2,mon3,mon4,mon5)
#输出
11 22 33 44 55 66

#注意：多一个值或者少一个值都不行
salaries = [11,22,33,44,55,66]
mon0,mon1,mon2,mon3,mon4,mon5=salaries
print(mon0,mon1,mon2,mon3,mon4,mon5)
#输出
11 22 33 44 55 66

salaries = [11,22,33,44,55,66]
mon0,mon1,*others=salaries  # 针对你不想要的变量用*_
mon0,mon1,*_=salaries
mon0,mon1,*_,mon_last=salaries  #获取前两个和最后一个
*_,x,y=salaries			#获取最后两个
print(mon0)
print(mon1)
print(others)
print(_)
#输出
11
22
[33, 44, 55, 66]

#课外知识，字典取值
x,y,z = {"k1":111,"k2":222,"k3":333}.values()
x,y,z = {"k1":111,"k2":222,"k3":333}.items()
print(x,y,z)
print(x)
```

### 逻辑运算符

```python
#   (1) not：对紧跟其后的那个条件的结果取反
print(not True) #False
print(not 10 > 3)   #False
print(not 10)   #True
#   (2) and：用来连接左右两个条件，左右两个条件的结果都为True是，and的最终结果才为True
print(True and 10 > 3)  #True
#   (3) or：用来连接左右两个条件，左右两个条件的结果但凡有一个True时，or的最终结果才为True
print(10 < 3 or 10 == 10)   #True

#	ps：偷懒原则==短路运算
#	条件1 and 条件2 and 条件3
#	条件1 or 条件2 or 条件3

#	优先级：not > and > or
res1 = 3>4 and 4>3 or not 1==3 and 'x' == 'x' or 3>3	#True
res2 = (3>4 and 4>3) or (not 1==3 and 'x' == 'x') or 3>3	#True
res3 = 3<4 and (4>3 or not (1==3 and 'x' == 'x') )		#True
# 了解
print(1 and 0)	# 0
print(1 and "abc" and 333)	# 333
print(False and True or True)	# True
print(0 and 2 or 1)	# 1
```

## 流程控制

### if判断

```python
'''
接收用户输入的用户名
接收用户输入的密码
判断 输入的用户名 等于 正确的用户名 并且 输入的密码 等于正确的密码：
    告诉用户登录成功
否则：
    告诉用户账号名或密码输入错误

if判断的完整的语法
if 条件1:
    代码1
    代码2
    代码3
    ...
elif 条件2:
    代码1
    代码2
    代码3
    ...
elif 条件3:
    代码1
    代码2
    代码3
    ...
...
else:
    代码1
    代码2
    代码3
    ...
    
# 语法1
'''
if 条件1:
    代码1
    代码2
    代码3
    ...
'''
# 语法2
'''
if 条件1:
    代码1
    代码2
    代码3
    ...
else:
    代码1
    代码2
    代码3
    ...
'''
# 语法3
'''
if 条件1:
    代码1
    代码2
    代码3
    ...
elif 条件2:
    代码1
    代码2
    代码3
    ...
elif 条件3:
    代码1
    代码2
    代码3
    ...
...
'''
# 语法4（if判断是可以嵌套的）
'''
if 条件1:
    if 条件1:
    	代码1
    代码2
    代码3
    ...
'''
'''
#	案例1:
db_name = "xiaoyunwei"
db_pwd = "abc@123"
name = input("用户名：")
pwd = input("密码：")

if name == db_name and pwd == db_pwd:
    print("登录成功")
else:
    print("登录失败")

#	案例2：
# 如果：成绩>=90,那么:优秀
# 如果成绩>=80且<90,那么:良好
# 如果成绩>=70且<80,那么:普通
# 其他情况：很差

chengji = input("请输入您的成绩：")
chengji = int(chengji)
if chengji >= 90:
    print("优秀")
elif chengji >= 80 and chengji < 90:
    print("良好")
elif chengji >= 70 and chengji < 80:
    print("普通")
else:
    print("很差")
#其他方法1    
if chengji >= 90:
    print("优秀")
elif chengji >= 80:
    print("良好")
elif chengji >= 70:
    print("普通")
else:
    print("很差")
#其他方法2
if chengji >= 90:
    print("优秀")
elif 80 <= chengji < 90:
    print("良好")
elif 70 <= chengji < 80:
    print("普通")
else:
    print("很差")
    
#	案例3:
age = 19
height = 1.7
gender = "female"
is_beautiful = True
if 18 < age < 26 and 1.6 < height < 1.8 and gender == "female" and is_beautiful:
    print("开始表白。。。")
else:
    print("你是个好人。。。")
print("其他代码。。。")
```

### while循环

```python
"""

while 条件:
    代码1
    代码2
    代码3
    ...

"""
# 1、基本使用
print('start...')
count = 0
while count < 5:
    print(count)
    count+=1
print('end...')
#输出
start...
0
1
2
3
4
end...

# 2、死循环
while 1:
    print("hello")

# 3、用户案例

db_name = "xiaoyunwei"
db_pwd = "abc@123"

while True:
    name = input("用户名：")
    pwd = input("密码：")

    if name == db_name and pwd == db_pwd:
        print("登录成功")
    else:
        print("登录失败")

# 4、结束while循环
# (1)把条件改成False
db_name = "xiaoyunwei"
db_pwd = "abc@123"
tag = True
while tag:
    name = input("用户名：")
    pwd = input("密码：")

    if name == db_name and pwd == db_pwd:
        print("登录成功")
        tag = False
    else:
        print("登录失败")
    print('========================')

# (2)break会直接结束本层循环
db_name = "xiaoyunwei"
db_pwd = "abc@123"
tag = True
while tag:
    name = input("用户名：")
    pwd = input("密码：")

    if name == db_name and pwd == db_pwd:
        print("登录成功")
        # tag = False
        break
    else:
        print("登录失败")
    print('========================')

tag = True
while tag:
    break
    while tag:
        break
        while tag:
            break

tag = True
while tag:
    tag = False
    while tag:
        tag = False
        while tag:
            tag = False
            
# 5、while循环的嵌套
db_name = "xiaoyunwei"
db_pwd = "abc@123"
tag = True
while tag:
    name = input("用户名：")
    pwd = input("密码：")

    if name == db_name and pwd == db_pwd:
        print("登录成功")
        while tag:
            print("""
                0 退出
                1 提现
                2 转账
                3 查询余额
                4 修改密码
                """)
            choice = input("请输入您的命令编号：")
            if choice == "0":
                # break
                tag = False
            elif choice == "1":
                print('=============>提现功能<================')
            elif choice == "2":
                print('=============>转账功能<================')
            else:
                print('=============>非法指令<================')
        break
    else:
        print("登录失败")
    print('========================')
    
# 6、while+contiune(会众制本次循环直接进入下一次)
conut = 0
while conut < 5:
    if conut == 3:
        # break
        conut += 1
        continue    #强调：与continue同一级别的后续代码永远不会运行
    print(conut)
    conut+=1

db_name = "xiaoyunwei"
db_pwd = "abc@123"

while True:
    name = input("用户名：")
    pwd = input("密码：")

    if name == db_name and pwd == db_pwd:
        print("登录成功")
    else:
        print("登录失败")
        # continue  # 此处不加continue也会进入下一次，不要画蛇添足
        
# 7、while+else
# 如果while循环不是被break干掉的，那么while的结束都算正常死亡
count = 0
while count < 5:
    if count == 3:
        # count+=1
        # continue
        break
    print(count)
    count+=1
else:
    print("else会在while循环正常死亡之后运行")
```

**1 练习题**

1. 简述编译型与解释型语言的区别，且分别列出你知道的哪些语言属于编译型，哪些属于解释型

2. 执行 Python 脚本的两种方式是什么（交互式、源文件）

3. Pyhton 单行注释和多行注释分别用什么?（#，''''''）

4. 布尔值分别有什么?（True\False）

5. 声明变量注意事项有那些?（python不需要声明变量，因为python是动态类型的语言）

6. 如何查看变量在内存中的地址?（id()）

7. 写代码

   1. 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败!

   ```python
   inp_name = input("your names:")
   inp_pwd = input("your password:")
   
   if inp_name == "seven" and inp_pwd == "123":
       print("Success！")
   else:
       print("ERROR!")
   ```

   2. 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次

   ```python
   count = 0
   while count < 3:
       inp_name = input("your names:")
       inp_pwd = input("your password:")
       if inp_name == "seven" and inp_pwd == "123":
           print("Success！")
           break
       else:
           count+=1
           print("ERROR!")
   ```

   3. 实现用户输入用户名和密码,当用户名为 seven 或 alex 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次

   ```python
   count = 0
   while count < 3:
       inp_name = input("your names:")
       inp_pwd = input("your password:")
       db_name = ["seven","alex"]
       db_pwd = '123'
   
       if inp_name in db_name and inp_pwd == db_pwd:
           print("Success！")
           break
       else:
           count+=1
           print("ERROR!")
   ```

8. 写代码
   a. 使用while循环实现输出2-3+4-5+6...+100 的和

   ```python
   sum = 0
   x = 1
   while x < 101:
       sum = sum + x
       x+=1
   print(sum)
   ```

   b. 使用 while 循环实现输出 1,2,3,4,5, 7,8,9, 11,12 使用 while 循环实现输出 1-100 内的所有奇数

   e. 使用 while 循环实现输出 1-100 内的所有偶数

   ```python
   #偶数
   a=100
   s=0
   
   while a>0:
       a=a-1
       if a % 2 == 0:
           print(a,end=' ') #end=''的作用是打印数字时不会换行，可以并排阅读。
           s+=a
   print('\n偶数和是：',s,'\n')
   
   #奇数
   b=100
   u=0
   while b>0:
       b=b-1
       if b % 2 != 0:
           print(b,end=' ')
           u+=b
   print('\n奇数和是：',u)
   
   #自己写的
   a = 100
   s = 0
   
   while a > 0:
       a = a - 1
       if a % 2 == 0:
           print(a)
           s+=a
   
   b = 100
   u = 0
   while b > 0:
       b = b - 1
       if b % 2 != 0:
           print(b)
           u+=b
   ```

9. 现有如下两个变量,请简述 n1 和 n2 是什么关系?

```
      n1 = 123456
      n2 = n1
      #	n2 是 n1的硬复制，如果n1变换了值，那么n2的值不会发生变化
```