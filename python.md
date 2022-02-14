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







