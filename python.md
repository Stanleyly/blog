### 深浅拷贝


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


### Python函数参数的传递（参数是引用，但是按值传递）
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








