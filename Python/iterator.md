# 魔法方法介绍
1. object.__iter__(self)
此方法在需要为容器创建迭代器时被调用。此方法应该返回一个新的迭代器对象，它能够逐个迭代容器中的所有对象。对于映射，它应该逐个迭代容器中的键。

迭代器对象也需要实现此方法；它们需要返回对象自身。

2. object.__reversed__(self)
此方法（如果存在）会被 reversed内置函数调用以实现逆向迭代。它应当返回一个新的以逆序逐个迭代容器内所有对象的迭代器对象。

3. object.__next__()
从容器中返回下一项。 如果已经没有项可返回，则会引发 StopIteration 异常。

# 可迭代(Iterable)
如果一个对象具备有 __iter__()  或者 __getitem__() 其中任何一个魔术方法的话，这个对象就可以称为是可迭代的。
其中，__iter__() 的作用是可以让 for 循环遍历，而 __getitem__()  方法可以让实例对象通过 [index] 索引的方式去访问实例中的元素。所以，List、Tuple、Dictionary、String 等数据类型都是可迭代的。

# 迭代器(Iterator)
如果一个对象同时有__iter__()和__next__()魔术方法的话，这个对象就可以称为是迭代器。
__iter__() 的作用前面我们也提到过，是可以让for循环遍历。而 __next__()方法是让对象可以通过 next(实例对象) 的方式访问下一个元素。
List、Tuple、Dictionary、String 等数据类型虽然是可迭代的，但都不是迭代器，因为他们都没有 next( )方法。

一个迭代器(Iterator)对象不仅可以在 for 循环中使用，还可以通过内置函数 next() 函数进行调用。

# 如何判断可迭代(iterable) & 迭代器(iterator)
借助Python中的isinstance(object, classinfo)函数来判断一个对象是否是一个已知类型。
```
from collections import Iterable  
from collections import Iterator

print(f"List is 'Iterable': {isinstance([], Iterable)}")  
print(f"Tuple is 'Iterable': {isinstance((), Iterable)}")  
print(f"Dict is 'Iterable': {isinstance({}, Iterable)}")  
print(f"String is 'Iterable': {isinstance('', Iterable)}")

print("="*25)

print(f"List is 'Iterator': {isinstance([], Iterator)}")  
print(f"Tuple is 'Iterator': {isinstance((), Iterator)}")  
print(f"Dict is 'Iterator': {isinstance({}, Iterator)}")  
print(f"String is 'Iterator': {isinstance('', Iterator)}")

# 输出如下：
# List is 'Iterable': True
# Tuple is 'Iterable': True
# Dict is 'Iterable': True
# String is 'Iterable': True
# =========================
# List is 'Iterator': False
# Tuple is 'Iterator': False
# Dict is 'Iterator': False
# String is 'Iterator': False
```

通过对定义的分析和比较我们得知：迭代器都是可迭代的（因为迭代器都包含__iter__()函数），但可迭代的不一定是迭代器（因为未必每个可迭代就包含__next__()方法）。

# 创建一个迭代器
所以只要定义了一个类并在类中实现 __iter__() 和 __next__() 方法，那么这个类就可以当做是一个迭代器了。

```
from collections import Iterator

class Data:  
    def __init__(self, x):
        self.x = x

    def __iter__(self):
        return self

    def __next__(self):
        if self.x >= 10:
            raise StopIteration
        else:
            self.x += 1
            return self.x

data = Data(0)

print(f"data is 'Iterator': {isinstance(data, Iterator)}")
# 输出如下：
# data is 'Iterator': True
```


# for 循环本质
for循环称为迭代器循环，in 后必须是可迭代的对象。
```
for i in 'hello':
    print(i)
```
可以看作是：

```
s = 'hello'
iter_s = s.__iter__()

while True:
    try:
        print(iter_s.__next__())
    except StopIteration:
        break
```
更好的例子：
```
from collections import Iterator

class Data:  
    def __init__(self, x):
        self.x = x

    def __iter__(self):
        return self

    def __next__(self):
        if self.x >= 10:
            raise StopIteration
        else:
            self.x += 1
            return self.x

data = Data(0)

for d in data:  
    print(d)

# 输出如下：
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10
```
但是在实际的 for 循环中不会引发异常，for 循环会将异常作为一个中断命令，从而停止循环。


# 无限迭代器
迭代器对象中的项目不必都是可耗尽的，可以是无限迭代器(永远不会结束)。 处理这样的迭代器时一定要小心。
```
from collections import Iterator

class Data:  
    def __init__(self, x):
        self.x = x

    def __iter__(self):
        return self

    def __next__(self):
        self.x += 1
        return self.x

data = Data(0)

for d in data:  
    print(d)
```
当迭代这些类型的无限迭代器时，请注意指定终止条件。

# 逆向迭代器
反向迭代仅仅当对象的大小可预先确定或者对象实现了 __reversed__() 的特殊方法时才能生效。
```
class  MyNumbers: 
    
    def __init__(self):
        self.flag=True  
        pass

        
    def __iter__(self):
        self.a=0
        return self
    
    def __reversed__(self):
        self.a=0
        self.flag=not self.flag
        return self
    
    def __next__(self):
        if self.flag:
           x=self.a+1
           if self.a>=5:
               raise StopIteration
        else:
           x=5-self.a
           if self.a>=5:
               raise StopIteration
        self.a+=1       
        return x   
            
            
myclass = MyNumbers()  
myiter = iter(myclass)  
print('iter-next')
for  x  in  myiter: 
    print(x)

print('reversed-next')
myrv=reversed(myclass)

print(next(myrv))
print(next(myrv))
print(next(myrv))
print(next(myrv))
print(next(myrv))

print('reversed-reversed')
myrv=reversed(myclass)
for i in myrv:
    print(i)
```
本例中直接实现了iter和reversed 两种方法。主要设置一个标志位，通过__reversed__改变标志位来设置是正序输出还是反序输出，通过多次调用reversed可以进行反转。

# 可迭代对象转迭代器对象
List、Tuple、Dictionary、String 等数据类型虽然是可迭代的，但都不是迭代器。
通过 iter() 方法可以将其转为迭代器对象。
```
from collections.abc import Iterable  
from collections.abc import Iterator

list_one = [1,2,3]
print(isinstance(list_one,Iterable))
print(isinstance(list_one,Iterator))
it_list = iter(list_one)
itr_list = list_one.__iter__()
print(isinstance(it_list,Iterable))
print(isinstance(it_list,Iterator))
print(isinstance(itr_list,Iterable))
print(isinstance(itr_list,Iterator))
print(next(it_list))
print(it_list.__next__())
print(next(itr_list))
print(itr_list.__next__())

# True
# False
# True
# True
# True
# True
# 1
# 2
# 1
# 2

```

iter(obj)      等同于 obj.__iter__()
next(obje)  等同于 obje.__next__()

# 迭代器优缺点：
- 优点：迭代器对象表示的是一个数据流，可以在需要时才去调用next来获取一个值；因而本身在内存中始终只保留一个值，对于内存占用小可以存放无限数据流。优于其他容器需要一次将所有元素都存放进内存，如：列表、集合、字典...等
- 缺点：1.无法获取存放的元素长度，除非取完计数。2.只能向后取值，next()永远返回的是下一个值。取值不灵活，无法取出指定值(无法像字典的key,或列表的下标)，而且迭代器的生命周期是一次性的元素被迭代完则生命周期结束

# 生成对象为迭代器的函数
enumerate() 、zip()、map()、filter() 生成的对象都为迭代器

```
from collections.abc import Iterator

def add(x,y,z):
    return x+1

list1 = [1,2,3]
list2 = [1,2,3]
en = enumerate(list1)
print(isinstance(en,Iterator))

zi = zip(list1,list2)
print(isinstance(zi,Iterator))

ma = map(add,list1)
print(isinstance(ma,Iterator))

fi = filter(lambda x: x>=2,list1)
print(isinstance(fi,Iterator))

# Ture
# Ture
# Ture
# Ture
```
## zip()  ： 同时迭代多个序列
同时迭代多个序列，每次分别从一个序列中取一个元素。
zip(a, b) 会生成一个可返回元组 (x, y) 的迭代器，其中x来自a，y来自b。 一旦其中某个序列到底结尾，迭代宣告结束。 因此迭代长度跟参数中最短序列长度一致。
```
a = [1, 2, 3]
b = ['w', 'x', 'y', 'z']
for i in zip(a,b):
...     print(i)
...
# (1, 'w')
# (2, 'x')
# (3, 'y')
```

拓展：如果希望得到的是最长序列，即没有值可以自动添加默认值的可以考虑使用 itertools.zip_longest() 函数来代替。
```
for i in zip_longest(a, b, fillvalue=0):
    print(i)
...
# (1, 'w')
# (2, 'x')
# (3, 'y')
# (0, 'z')
```
fillvalue 的值没有会默认为 None。

## enumerate() ：序列上索引值迭代
迭代一个序列的同时跟踪正在被处理的元素索引。
为了按传统行号输出(行号从1开始)，你可以传递一个开始参数（默认从0开始）：

```
my_list = ['a', 'b', 'c']
for idx, val in enumerate(my_list, 1):
    print(idx, val)
...
# 1 a
# 2 b
# 3 c
```
enumerate() 函数返回的是一个 enumerate 对象实例， 它是一个迭代器，返回连续的包含一个计数和一个值的元组， 元组中的值通过在传入序列上调用 next() 返回。

[Python中的迭代器与可迭代](http://anders.wang/python-iterable-iterator/)
[Python迭代器和反转迭代器的一点思考](https://zhuanlan.zhihu.com/p/350948181)
[Python迭代器](https://www.yiibai.com/python/iterator.html)
[python3-cookbook](https://python3-cookbook.readthedocs.io/zh_CN/latest/c04/p11_iterate_over_multiple_sequences_simultaneously.html)
