# Python 常见问题及错误
* [1 深浅拷贝](#1-深浅拷贝)
* [2 Python函数参数的传递](#2-Python函数参数的传递)
* [3 类变量和实例变量](#3-类变量和实例变量)
* [4 Python自省](#4-Python自省)
* [5 Flask和Django的区别](#5-Flask和Django的区别)
* [6 字典推导式](#6-字典推导式)
* [7 字符串格式化](#7-字符串格式化)
* [8 Python中单下划线和双下划线](#8-Python中单下划线和双下划线)
* [9 迭代器和生成器](#9-迭代器和生成器)

## 1 深浅拷贝
+ **明确对象**
  +  不可更改（immutable）：string、tuple、numbers
  +  可更改（mutable）：list、dict、set
+ 直接赋值：就是对象的引用
+ 浅拷贝：一个新的对象对原始对象的属性值进行精确地拷贝，如果拷贝的是基本数据类型，拷贝的就是基本数据类型的值；如果拷贝的是引用数据类型，拷贝的就是内存地址。**浅拷贝后，如果对引用对象做出更改，其也会随之更改，但是基本数据类型更改，其不会改变。**
+ 深拷贝：就是把原数据复制一份，在复制的数据上随意改动不会影响到其原数据。

```python
import copy
# 原始对象
a = [1, 2, 3, 4, ['a', 'b']] 

# 赋值
b = a
# 浅拷贝
c = copy.copy(a)
# 深拷贝
d = copy.deepcopy(a)

a.append(5) #修改对象a
a[4].append('c') #修改对象a中的['a', 'b']数组对象

print 'a = ', a
print 'b = ', b
print 'c = ', c
print 'd = ', d
```
运行结果：
<img width="355" alt="image" src="https://user-images.githubusercontent.com/45594667/153817160-c74c1d68-8781-4861-a82c-470cd0ffeba0.png">


## 2 Python函数参数的传递

**(参数是引用，但是按值传递)**
+ 区分引用传递和值传递
  - 传入的参数是一个对象的引用（但是引用是按照值传递）
  - 值传递：形参改变不影响实参
  - 引用传递：形参改变，实参也会改变

+ 当一个引用传递给函数的时候,函数自动复制一份引用,这个函数里的引用和外边的引用没有半毛关系了.所以第一个例子里函数把引用指向了一个不可变对象,当函数返回的时候,外面的引用没半毛感觉.而第二个例子就不一样了,函数内的引用指向的是可变对象,对它的操作就和定位了指针地址一样,在内存里进行修改.

```python
# 例子1：传入不可更改对象，string、tuple、numbers
def fun(a):
    print ("func_in",id(a)) # id:4535200496
    a = 2
    print ("re-point", id(a)) # id:4535200528

print ("func_out", id(a), id(1)) # id:4535200496 4535200496

fun(a)
print (a)

# 例子2：传入可更改对象，list、dict、set
a = []

def fun(a):
    print("func_in", id(a)) # id:4479482752
    a.append(1)

print ("func_out", id(a)) # id:4479482752
fun(a)
print (a)

```
运行结果：

不可变对象：

<img width="242" alt="image" src="https://user-images.githubusercontent.com/45594667/153855185-d48b0a92-f2d5-40cf-8722-8e16c418edb1.png">

可变对象：

<img width="161" alt="image" src="https://user-images.githubusercontent.com/45594667/153855105-b9178874-8f2a-426c-b93c-d532f38a505d.png">

## 3 类变量和实例变量

+ 类变量：是可在类的所有实例之间共享的值（也就是说，它们不是单独分配给每个实例的）
+ 实例变量：实例化之后，每个实例单独拥有的变量

```python
# 类变量
class Test(object):
	num_of_instance = 0
	def __init__(self, name):
		self.name = name
		Test.num_of_instance +=1
		
if __name__ == '__main__':
	print Test.num_of_instance   # 0
    t1 = Test('jack')  
    print Test.num_of_instance   # 1
    t2 = Test('lucy')  
    print t1.name , t1.num_of_instance  # jack 2
    print t2.name , t2.num_of_instance  # lucy 2

# 实例变量
class Person:
    name="aaa"

p1=Person()
p2=Person()
p1.name="bbb"
print p1.name  # bbb
print p2.name  # aaa
print Person.name  # aaa
```


## 4 Python自省
自省：运行时能能够获得对象的类型

```python
a = [1, 2, 3]
b = {'a':1, 'b':2, 'c':3}
c = True
print (type(a), type(b), type(c)) 
print (isinstance(a, list))

```

## 5 Flask和Django的区别
+ ##### 流行度：
Django比Flask更为流行**一些复杂的web程序更多使用的是Django**，使用Django强大的功能来快速构建和部署复杂的Web应用程序。同样，开发人员使用Flask来加速使用固定内容的网站的开发
+ ##### 灵活性：
Django 可在不使用太多第三方库和工具的条件下开发各种优秀的Web应用程序，Flask是一个扩展性很好的Web框架，可以使用各种Web开发库和工具来灵活地开发Web应用程序。就是说相比较Django，Flask可以较为轻松的方便开发人员使用自己的技术栈。
+ 总结：
  + Flask提供了灵活性，简单性和细粒度的控制。
  + Flask不受限制，让你决定如何实现应用程序。
  + Django为你的Web应用程序开发提供了管理面板，数据库界面，目录结构和ORM的全方位体验。


## 6 字典推导式、列表推导式和集合推导式
```python
# 字典推导式
d = {key: value for (key, value) in interable}
# 列表推导式
l = [i * 2 for i in range(10) if i % 2 ==0 ]
# 元祖推导式
t = (i * 2 for i in range(10))
print t #<generator object <genexpr> at 0x7fefe5989af0>
此时t是一个生成器对象，所以想要元组
print(tuple(t)) # (0, 2, 4, 6, 8, 10, 12, 14, 16, 18)
```


## 7 字符串格式化
+ %
+ .format
```python 
# 基本方法
print ('We are the {} who say "{}"!'.format('knights', 'Ni')) # We are the knights who say "Ni"!
print ('{0} and {1}'.format('spam', 'egg') # spam and egg
print ('{1} and {0}'.format('spam', 'egg') # egg and spam
# 方法中关键字参数名引用值
print ('This {food} is {adj}.'.format(food = 'spam', adj = 'absolutely horrible'))# This spam is absolutely horrible.
```

## 8 Python中单下划线和双下划线
```python
class MyClass():
    def __init__(self):
        self.__superprivate = "Hello"
        self._semiprivate = ", world!"
        
mc = MyClass()
print mc.__superprivate # AttributeError: MyClass instance has no attribute '__superprivate'
print mc._semiprivate # , world!
promt mc.__dict__ # {'_MyClass__superprivate': 'Hello', '_semiprivate': ', world!'}
```
+ `__ foo__`:一种约定，Python内部的名字，用来区别其他用户自定义的命名，以防冲突；如：`__init__()`,`__del()__`,`__call()__`等
+ `_foo`:一种约定，用来指定变量私有，不能用from module import *导入，其他和公有一样访问
+ `__foo`:有真正的意义，解析器用`_classname__foo`来代替这个名字，以区别和其他类相同的命名，无法直接像公有成员一样随便访问，通过对象._类名__xxx这样的方式来访问

## 9 迭代器和生成器
