# 元组
* 元组和列表类似，但属于**不可变序列**，元组一旦创建，用任何方法都不可以修改其元素。
* 元组的定义方式和列表相同，但定义时所有元素是放在**一对圆括号**“（）”中，而不是方括号中。

## 元组创建与删除

### 使用“=”将一个元组赋值给变量

```javascript{.line-numbers}
>>>a_tuple = ('a', 'b', 'mpilgrim', 'z', 'example')
>>> a_tuple
('a', 'b', 'mpilgrim', 'z', 'example')
>>> a = (3)
>>> a
3
>>> a = (3,)                            #包含一个元素的元组，最后必须多写个逗号
>>> a
(3,)
>>> a = 3,                              #也可以这样创建元组
>>> a
(3,)
>>> x = () #空元组
```

### 使用tuple函数将其他序列转换为元组

```javascript{.line-numbers}
>>> tuple('abcdefg')       #把字符串转换为元组
('a', 'b', 'c', 'd', 'e', 'f', 'g')
>>> aList
[-1, -4, 6, 7.5, -2.3, 9, -11]
>>> tuple(aList)     #把列表转换为元组
(-1, -4, 6, 7.5, -2.3, 9, -11)
>>> s = tuple()      #空元组
>>> s
()
```

使用del可以删除元组对象，不能删除元组中的元素

## **元组与列表的区别**

* 元组中的数据一旦定义就不允许更改。
* 元组没有append()、extend()和insert()等方法，无法向元组中添加元素。
* 元组没有remove()或pop()方法，也无法对元组元素进行del操作，不能从元组中删除元素。
* 从效果上看，tuple( )冻结列表，而list( )融化元组。
* 元组的速度比列表更快。如果定义了一系列常量值，而所需做的仅是对它进行遍历，那么一般使用元组而不用列表。
* 元组对不需要改变的数据进行“写保护”将使得代码更加安全。
* 元组可用作字典键（特别是包含字符串、数值和其它元组这样的不可变数据的元组）。列表永远不能当做字典键使用，因为列表不是不可变的。

## 序列解包

可以使用序列解包功能对多个变量同时赋值

```javascript{.line-numbers}
>>> x, y, z = 1, 2, 3    #多个变量同时赋值
>>> v_tuple = (False, 3.5, 'exp')
>>> (x, y, z) = v_tuple
>>> x, y, z = v_tuple
>>> x, y, z = range(3)   #可以对range对象进行序列解包
>>> x, y, z = iter([1, 2, 3])    #使用迭代器对象进行序列解包
>>> x, y, z = map(str, range(3))    #使用可迭代的map对象进行序列解包
>>> a, b = b, a     #交换两个变量的值
>>> x, y, z = sorted([1, 3, 2])   #sorted()函数返回排序后的列表
>>> a, b, c = 'ABC'       #字符串也支持序列解包
```

序列解包对于列表和字典同样有效

```javascript{.line-numbers}
>>> s = {'a':1, 'b':2, 'c':3}
>>> b, c, d = s.items()
>>> d
('c', 3)
>>> b, c, d = s    #使用字典时不用太多考虑元素的顺序
>>> b
'c'
>>> b, c, d = s.values()
>>> print(b, c, d)
1 3 2
```

序列解包遍历多个序列

```javascript{.line-numbers}
>>> keys = ['a', 'b', 'c', 'd']
>>> values = [1, 2, 3, 4]
>>> for k, v in zip(keys, values):
	  print((k, v), end=' ')
('a', 1) ('b', 2) ('c', 3) ('d', 4) 
```

使用序列解包遍历enumerate对象

```javascript{.line-numbers}
>>> x = ['a', 'b', 'c']
>>> for i, v in enumerate(x):
	  print('The value on position {0} is {1}'.format(i,v))

The value on position 0 is a
The value on position 1 is b
The value on position 2 is c

>>> aList = [1,2,3]
>>> bList = [4,5,6]
>>> cList = [7,8,9]
>>> dList = zip(aList, bList, cList)
>>> for index, value in enumerate(dList):
	    print(index, ':', value)

0 : (1, 4, 7)
1 : (2, 5, 8)
2 : (3, 6, 9)
```

Python 3.5还支持下面用法的序列解包

```javascript{.line-numbers}
>>> print(*[1, 2, 3], 4, *(5, 6))
1 2 3 4 5 6
>>> *range(4),4
(0, 1, 2, 3, 4)
>>> {*range(4), 4, *(5, 6, 7)}
{0, 1, 2, 3, 4, 5, 6, 7}
>>> {'x': 1, **{'y': 2}}
{'y': 2, 'x': 1}
```
## 生成器推导式

* 生成器推导式的结果是一个生成器对象。使用生成器对象的元素时，可以根据需要将其转化为列表或元组，也可以使用生成器对象__next__()方法或内置函数next()进行遍历，或者直接将其作为迭代器对象来使用。
* 生成器对象具有惰性求值的特点，只在需要时生成新元素，比列表推导式具有更高的效率，空间占用非常少，尤其适合大数据处理的场合。
* 不管用哪种方法访问生成器对象，都无法再次访问已访问过的元素。
* 使用生成器对象__next__()方法或内置函数next()进行遍历

```javascript{.line-numbers}
>>> g = ((i+2)**2 for i in range(10))     #创建生成器对象
>>> g
<generator object <genexpr> at 0x0000000003095200>
>>> tuple(g)                                         #将生成器对象转换为元组
(4, 9, 16, 25, 36, 49, 64, 81, 100, 121)
>>> list(g)                                             #生成器对象已遍历结束，没有元素了
[] 
>>> g = ((i+2)**2 for i in range(10))      #重新创建生成器对象
>>> g.__next__()                             #使用生成器对象的__next__()方法获取元素
4
>>> g.__next__()                             #获取下一个元素
9
>>> next(g)                                      #使用函数next()获取生成器对象中的元素
16
```

使用for循环直接迭代生成器对象中的元素

```javascript{.line-numbers}
>>> g = ((i+2)**2 for i in range(10))
>>> for item in g:    #使用循环直接遍历生成器对象中的元素
       print(item, end=' ')
4 9 16 25 36 49 64 81 100 121 
>>> x = filter(None, range(20))   #filter对象也具有类似的特点
>>> 5 in x
True
>>> 2 in x    #不可再次访问已访问过的元素
False
>>> x = map(str, range(20))      #map对象也具有类似的特点
>>> '0' in x
True
>>> '0' in x          #不可再次访问已访问过的元素
False
```

# 字典
* 字典是**无序可变**序列。
* 定义字典时，每个元素的键和值用冒号分隔，元素之间用逗号分隔，所有的元素放在一对大括号“｛｝”中。
* 字典中的**键可以为任意不可变数据**，比如整数、实数、复数、字符串、元组等等。
* globals()返回包含当前作用域内所有全局变量和值的字典
* locals()返回包含当前作用域内所有局部变量和值的字典

## 字典创建与删除

使用=将一个字典赋值给一个变量

```javascript{.line-numbers}
>>> a_dict = {'server': 'db.diveintopython3.org', 'database': 'mysql'}
>>> a_dict
{'database': 'mysql', 'server': 'db.diveintopython3.org'}
>>> x = {}                     #空字典
>>> x
{}
```

使用dict利用已有数据创建字典：

```javascript{.line-numbers}
>>> keys = ['a', 'b', 'c', 'd']
>>> values = [1, 2, 3, 4]
>>> dictionary = dict(zip(keys, values))
>>> dictionary
{'a': 1, 'c': 3, 'b': 2, 'd': 4}
>>> x = dict() #空字典
>>> x
{}
```

使用dict根据给定的键、值创建字典

```javascript{.line-numbers}
>>> d = dict(name='Dong', age=37)
>>> d
{'age': 37, 'name': 'Dong'}
```

以给定内容为键，创建值为空的字典

```javascript{.line-numbers}
>>> adict = dict.fromkeys(['name', 'age', 'sex'])
>>> adict
{'age': None, 'name': None, 'sex': None}
```

可以使用del删除整个字典

## 字典元素的读取

以键作为下标可以读取字典元素，若键不存在则抛出异常

```javascript{.line-numbers}
>>> aDict = {'name':'Dong', 'sex':'male', 'age':37}
>>> aDict['name']
'Dong'
>>> aDict['tel']                                 #键不存在，抛出异常
Traceback (most recent call last):
  File "<pyshell#53>", line 1, in <module>
    aDict['tel']
KeyError: 'tel'
```

使用字典对象的get方法获取指定键对应的值，并且可以在键不存在的时候返回指定值。

```javascript{.line-numbers}
>>> print(aDict.get('address'))
None
>>> print(aDict.get('address', 'SDIBT'))
SDIBT
>>> aDict['score'] = aDict.get('score',[])
>>> aDict['score'].append(98)
>>> aDict['score'].append(97)
>>> aDict
{'age': 37, 'score': [98, 97], 'name': 'Dong', 'sex': 'male'}
```

* 使用字典对象的items()方法可以返回字典的键、值对列表
* 使用字典对象的keys()方法可以返回字典的键列表
* 使用字典对象的values()方法可以返回字典的值列表

```javascript{.line-numbers}
>>> aDict={'name':'Dong', 'sex':'male', 'age':37}
>>> for item in aDict.items():         #输出字典中所有元素
	   print(item)
('age', 37)
('name', 'Dong')
('sex', 'male')

>>> for key in aDict:                       #不加特殊说明，默认输出键
	print(key)
age
name
sex
>>> for key, value in aDict.items():             #序列解包用法
	   print(key, value)
age 37
name Dong
sex male

>>> aDict.keys()                                          #返回所有键
dict_keys(['name', 'sex', 'age'])

>>> aDict.values()                                       #返回所有值
dict_values(['Dong', 'male', 37])
```

## 字典元素的添加与修改

当以指定键为下标为字典赋值时，若键存在，则可以修改该键的值；若不存在，则表示添加一个键、值对。

```javascript{.line-numbers}
>>> aDict['age'] = 38                      #修改元素值
>>> aDict
{'age': 38, 'name': 'Dong', 'sex': 'male'}
>>> aDict['address'] = 'SDIBT'        #增加新元素
>>> aDict
{'age': 38, 'address': 'SDIBT', 'name': 'Dong', 'sex': 'male'}
```

使用字典对象的update方法将另一个字典的键、值对添加到当前字典对象

```javascript{.line-numbers}
>>> aDict
{'age': 37, 'score': [98, 97], 'name': 'Dong', 'sex': 'male'}
>>> aDict.items()
dict_items([('age', 37), ('score', [98, 97]), ('name', 'Dong'), ('sex', 'male')])
>>> aDict.update({'a':'a','b':'b'})
>>> aDict
{'a': 'a', 'score': [98, 97], 'name': 'Dong', 'age': 37, 'b': 'b', 'sex': 'male'}
```

* 使用del删除字典中指定键的元素
* 使用字典对象的clear()方法来删除字典中所有元素
* 使用字典对象的pop()方法删除并返回指定键的元素
* 使用字典对象的popitem()方法删除并返回字典中的一个元素

## 字典应用案例

首先生成包含1000个随机字符的字符串，然后统计每个字符的出现次数。

```javascript{.line-numbers}
>>> import string
>>> import random
>>> x = string.ascii_letters + string.digits + string.punctuation
>>> y = [random.choice(x) for i in range(1000)]
>>> z = ''.join(y)
>>> d = dict()                  #使用字典保存每个字符出现次数
>>> for ch in z:
	 d[ch] = d.get(ch, 0) + 1
```

也可以使用collections模块的defaultdict类来实现。

```javascript{.line-numbers}
>>> import string
>>> import random
>>> x = string.ascii_letters + string.digits + string.punctuation
>>> y = [random.choice(x) for i in range(1000)]
>>> z = ''.join(y)
>>> from collections import defaultdict
>>> frequences = defaultdict(int)
>>> frequences
defaultdict(<type 'int'>, {})
>>> for item in z:
    frequences[item] += 1
>>> frequences.items()
```

使用collections模块的Counter类可以快速实现这个功能，并且提供更多功能，例如查找出现次数最多的元素。

```javascript{.line-numbers}
>>> from collections import Counter
>>> frequences = Counter(z)
>>> frequences.items()
>>> frequences.most_common(1)          #出现次数最多的一个字符
[('A', 22)]
>>> frequences.most_common(3)
[('A', 22), (';', 18), ('`', 17)]
```

Counter对象用法示例

```javascript{.line-numbers}
>>> cnt = Counter()
>>> for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
       cnt[word] += 1
>>> cnt
Counter({'blue': 3, 'red': 2, 'green': 1})
>>> import re
>>> words = re.findall(r'\w+', open('hamlet.txt').read().lower())
>>> Counter(words).most_common(10)            #出现次数最多的10个单词
```

## 有序字典

Python内置字典是无序的，如果需要一个可以记住元素插入顺序的字典，可以使用collections.OrderedDict。

```javascript{.line-numbers}
>>> x = dict()                   #无序字典
>>> x['a'] = 3
>>> x['b'] = 5
>>> x['c'] = 8
>>> x
{'b': 5, 'c': 8, 'a': 3}
>>> import collections
>>> x = collections.OrderedDict() #有序字典
>>> x['a'] = 3
>>> x['b'] = 5
>>> x['c'] = 8
>>> x
OrderedDict([('a', 3), ('b', 5), ('c', 8)])
```

## 字典推导式

```javascript{.line-numbers}
>>> s = {x:x.strip() for x in ('  he  ', 'she    ', '    I')}
>>> s
{'  he  ': 'he', '    I': 'I', 'she    ': 'she'}
>>> for k, v in s.items():
	       print(k, ':', v)

  he   : he
    I : I
she     : she 
```

```javascript{.line-numbers}
>>> {i:str(i) for i in range(1, 5)}
{1: '1', 2: '2', 3: '3', 4: '4'}
>>> x = ['A', 'B', 'C', 'D']
>>> y = ['a', 'b', 'b', 'd']
>>> {i:j for i,j in zip(x,y)}
{'A': 'a', 'C': 'b', 'B': 'b', 'D': 'd'}
```

# 集合

* 集合是**无序可变**序列，使用一对大括号界定，**元素不可重复**，同一个集合中每个元素都是唯一的。
* 集合中只能包含数字、字符串、元组等不可变类型（或者说可哈希）的数据，而不能包含列表、字典、集合等可变类型的数据。

## 集合的创建与删除

直接将集合赋值给变量

```javascript{.line-numbers}
>>> a = {3, 5}
>>> a.add(7)                  #向集合中添加元素
>>> a
{3, 5, 7}
```

使用set将其他类型数据转换为集合

```javascript{.line-numbers}
>>> a_set = set(range(8,14))
>>> a_set
{8, 9, 10, 11, 12, 13}
>>> b_set = set([0, 1, 2, 3, 0, 1, 2, 3, 7, 8])     #自动去除重复
>>> b_set
{0, 1, 2, 3, 7, 8}
>>> c_set = set()                                              #空集合
>>> c_set
set()
```

使用del删除整个集合

当不再使用某个集合时，可以使用del命令删除整个集合。集合对象的pop()方法弹出并删除其中一个元素，remove()方法直接删除指定元素，clear()方法清空集合。

```javascript{.line-numbers}
>>> a = {1, 4, 2, 3}
>>> a.pop()
1
>>> a.pop()
2
>>> a
{3, 4}
>>> a.add(2)
>>> a
{2, 3, 4}
>>> a.remove(3)
>>> a
{2, 4}
```

## 集合操作

Python集合支持交集、并集、差集等运算

```javascript{.line-numbers}
>>> a_set = set([8, 9, 10, 11, 12, 13])
>>> b_set = {0, 1, 2, 3, 7, 8}
>>> a_set | b_set                             #并集
{0, 1, 2, 3, 7, 8, 9, 10, 11, 12, 13}
>>> a_set.union(b_set)                   #并集
{0, 1, 2, 3, 7, 8, 9, 10, 11, 12, 13}
>>> a_set & b_set                           #交集
{8}
>>> a_set.intersection(b_set)          #交集
{8}
>>> a_set.difference(b_set)             #差集
{9, 10, 11, 12, 13}
>>> a_set - b_set
{9, 10, 11, 12, 13}
>>> a_set.symmetric_difference(b_set)    #对称差集
{0, 1, 2, 3, 7, 9, 10, 11, 12, 13}
>>> a_set ^ b_set
{0, 1, 2, 3, 7, 9, 10, 11, 12, 13}
>>> x = {1, 2, 3}
>>> y = {1, 2, 5}
>>> z = {1, 2, 3, 4}
>>> x.issubset(y)                                     #测试是否为子集
False
>>> x.issubset(z)
True
>>> {3} & {4}
set()
>>> {3}.isdisjoint({4})                               #如果两个集合的交集为空，返回True
True
```

集合包含关系测试

```javascript{.line-numbers}
>>> x = {1, 2, 3}
>>> y = {1, 2, 5}
>>> z = {1, 2, 3, 4}
>>> x < y                                        #比较集合大小/包含关系
False
>>> x < z                                         #真子集
True
>>> y < z
False
>>> {1, 2, 3} <= {1, 2, 3}                #子集
True
```

使用集合快速提取序列中单一元素

```javascript{.line-numbers}
>>> import random
>>> listRandom = [random.choice(range(10000)) for i in range(100)]
>>> noRepeat = []
>>> for i in listRandom :
	  if i not in noRepeat :
		 noRepeat.append(i)
>>> len(listRandom)
>>> len(noRepeat)
>>> newSet = set(listRandom)
```

## 集合运用案例

例2-1  生成不重复随机数的效率比较。

```javascript{.line-numbers}
import random
import time

def RandomNumbers(number, start, end):
    '''使用列表来生成number个介于start和end之间的不重复随机数'''
    data = []
    n = 0
    while True:
        element = random.randint(start, end)
        if element not in data:
            data.append(element)
            n += 1
        if n == number - 1:
            break
    return data

def RandomNumbers1(number, start, end):
    '''使用列表来生成number个介于start和end之间的不重复随机数'''
    data = []
    while True:
        element = random.randint(start, end)
        if element not in data:
            data.append(element)
        if len(data) == number:
            break
    return data

def RandomNumbers2(number, start, end):
    '''使用集合来生成number个介于start和end之间的不重复随机数'''
    data = set()
    while True:
        data.add(random.randint(start, end))
        if len(data) == number:
            break
    return data

start = time.time()
for i in range(10000):
    RandomNumbers(1000, 1, 10000)
print('Time used:', time.time()-start)

start = time.time()
for i in range(10000):
    RandomNumbers1(1000, 1, 10000)
print('Time used:', time.time()-start)

start = time.time()
for i in range(10000):
    RandomNumbers2(1000, 1, 10000)
print('Time used:', time.time()-start)
```

## 集合推导式

```javascript{.line-numbers}
>>> s = {x.strip() for x in ('  he  ', 'she    ', '    I')}
>>> s
{'I', 'she', 'he'}
```

# 再谈内置方法sorted()
* 列表对象提供了sort()方法支持原地排序，而内置函数sorted()返回新的列表，并不对原列表进行任何修改。
* sorted()方法可以对列表、元组、字典、range对象等进行排序。
* 列表的sort()方法和内置函数sorted()都支持key参数实现复杂排序要求。

```javascript{.line-numbers}
>>> persons = [{'name':'Dong', 'age':37}, {'name':'Zhang', 'age':40}, {'name':'Li', 'age':50}, {'name':'Dong', 'age':43}]
>>> print(persons)
[{'age': 37, 'name': 'Dong'}, {'age': 40, 'name': 'Zhang'}, {'age': 50, 'name': 'Li'}, {'age': 43, 'name': 'Dong'}]
#使用key来指定排序依据，先按姓名升序排序，姓名相同的按年龄降序排序
>>> print(sorted(persons, key=lambda x:(x['name'], -x['age'])))
[{'age': 43, 'name': 'Dong'}, {'age': 37, 'name': 'Dong'}, {'age': 50, 'name': 'Li'}, {'age': 40, 'name': 'Zhang'}]

>>> phonebook = {'Linda':'7750', 'Bob':'9345', 'Carol':'5834'}
>>> from operator import itemgetter
>>> sorted(phonebook.items(), key=itemgetter(1)) #按字典中元素值进行排序
[('Carol', '5834'), ('Linda', '7750'), ('Bob', '9345')]
>>> sorted(phonebook.items(), key=itemgetter(0)) #按字典中元素的键进行排序
[('Bob', '9345'), ('Carol', '5834'), ('Linda', '7750')]

>>> gameresult = [['Bob', 95.0, 'A'], ['Alan', 86.0, 'C'], ['Mandy', 83.5, 'A'], ['Rob', 89.3, 'E']]
>>> sorted(gameresult, key=itemgetter(0, 1)) #按姓名升序，姓名相同按分数升序排序
[['Alan', 86.0, 'C'], ['Bob', 95.0, 'A'], ['Mandy', 83.5, 'A'], ['Rob', 89.3, 'E']]
>>> sorted(gameresult, key=itemgetter(1, 0)) #按分数升序，分数相同的按姓名升序排序
[['Mandy', 83.5, 'A'], ['Alan', 86.0, 'C'], ['Rob', 89.3, 'E'], ['Bob', 95.0, 'A']]
>>> sorted(gameresult, key=itemgetter(2, 0)) #按等级升序，等级相同的按姓名升序排序
[['Bob', 95.0, 'A'], ['Mandy', 83.5, 'A'], ['Alan', 86.0, 'C'], ['Rob', 89.3, 'E']]

>>> gameresult = [{'name':'Bob', 'wins':10, 'losses':3, 'rating':75.0},
                              {'name':'David', 'wins':3, 'losses':5, 'rating':57.0},
                              {'name':'Carol', 'wins':4, 'losses':5, 'rating':57.0},
                              {'name':'Patty', 'wins':9, 'losses':3, 'rating':72.8}]
>>> sorted(gameresult, key=itemgetter('wins', 'name')) 
#按'wins'升序，该值相同的按'name'升序排序
[{'wins': 3, 'rating': 57.0, 'name': 'David', 'losses': 5}, {'wins': 4, 'rating': 57.0, 'name': 'Carol', 'losses': 5}, {'wins': 9, 'rating': 72.8, 'name': 'Patty', 'losses': 3}, {'wins': 10, 'rating': 75.0, 'name': 'Bob', 'losses': 3}]
```

根据另一个列表的值来对当前列表元素进行排序

```javascript{.line-numbers}
>>> list1 = ["what", "I'm", "sorting", "by"]
>>> list2 = ["something", "else", "to", "sort"]
>>> pairs = zip(list1, list2)
>>> pairs = sorted(pairs)
>>> pairs
[("I'm", 'else'), ('by', 'sort'), ('sorting', 'to'), ('what', 'something')]
>>> result = [x[1] for x in pairs]
>>> result
['else', 'sort', 'to', 'something']
```

# 复杂数据结构

* 在解决实际问题时，还经常需要用到其他复杂的数据结构，如堆、栈、队列、树、图等等。
* 有些结构Python已经提供，而有些则需要自己利用基本数据结构来实现。

## 堆

```javascript{.line-numbers}
>>> import heapq                    #heapq和random是Python标准库
>>> import random
>>> data=range(10)
>>> data
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> random.choice(data)             #随机选择一个元素
9
>>> random.shuffle(data)            #随机打乱顺序
>>> data
[6, 1, 3, 4, 9, 0, 5, 2, 8, 7]
>>> heap=[]
>>> for n in data:                  #建堆
    heapq.heappush(heap,n)
>>> heap
[0, 2, 1, 4, 7, 3, 5, 6, 8, 9]
>>> heapq.heappush(heap,0.5)        #入堆，自动重建
>>> heap
[0, 0.5, 1, 4, 2, 3, 5, 6, 8, 9, 7]
>>> heapq.heappop(heap)             #出堆，自动重建
0
>>> myheap=[1,2,3,5,7,8,9,4,10,333]
>>> heapq.heapify(myheap)             #建堆
>>> myheap
[1, 2, 3, 4, 7, 8, 9, 5, 10, 333]
>>> heapq.heapreplace(myheap,6)       #弹出最小元素，同时插入新元素
1
>>> myheap
[2, 4, 3, 5, 7, 8, 9, 6, 10, 333]
>>> heapq.nlargest(3, myheap)         #返回前3个最大的元素
[333, 10, 9]
>>> heapq.nsmallest(3, myheap)        #返回前3个最小的元素
[2, 3, 4]
```

## 队列

```javascript{.line-numbers}
>>> import queue        #queue是Python标准库
>>> q=queue.Queue()
>>> q.put(0)            #入队
>>> q.put(1)
>>> q.put(2)
>>> q.queue
deque([0, 1, 2])
>>> q.get()             #出队
0
>>> q.queue             #查看队列中的元素
deque([1, 2])
>>> q.get()
1
>>> q.queue
deque([2])
```

### queue模块还提供了“后进先出”队列和优先级队列。

```javascript{.line-numbers}
>>> from queue import Queue    #LILO队列
>>> q = Queue()                #创建队列对象
>>> q.put(0)                   #在队列尾部插入元素
>>> q.put(1)
>>> q.put(2)
>>> print(q.queue)             #查看队列中所有元素
deque([0, 1, 2])
>>> q.get()                    #返回并删除队列头部元素
0
>>> q.get()
1

>>> from queue import LifoQueue  #LIFO队列
>>> q = LifoQueue()              #创建LIFO队列对象
>>> q.put(1)                     #在队列尾部插入元素
>>> q.put(2)
>>> q.put(3)
>>> q.queue                      #查看队列中所有元素
[1, 2, 3]
>>> q.get()                      #返回并删除队列尾部元素
3
>>> q.get()
2
>>> q.queue
[1]
>>> q.get()                      #对空队列调用get()方法会阻塞当前线程

>>> from queue import PriorityQueue   #优先级队列
>>> q = PriorityQueue()                         #创建优先级队列对象
>>> q.put(3)                       #插入元素
>>> q.put(8)                       #插入元素
>>> q.put(100)
>>> q.queue                       #查看优先级队列中所有元素
[3, 8, 100]
>>> q.put(1)                       #插入元素，自动调整优先级队列
>>> q.put(2)
>>> q.queue
[1, 2, 100, 8, 3]
>>> q.get()                        #返回并删除优先级最低的元素
1
>>> q.get()                        #请多执行几次该语句并观察返回的数据
2
```

### Python标准库collections提供了双端队列deque

```javascript{.line-numbers}
>>> from collections import deque
>>> q = deque(maxlen=5)               #创建双端队列
>>> for item in [3, 5, 7, 9, 11]:          #添加元素
	q.append(item)
>>> q.append(13)                             #队列满，自动溢出
>>> q.append(15)
>>> q
deque([7, 9, 11, 13, 15], maxlen=5)
>>> q.appendleft(5)                          #从左侧添加元素，右侧自动溢出
>>> q
deque([5, 7, 9, 11, 13], maxlen=5)
```

### 封装列表自行定义队列

```javascript{.line-numbers}
# -*- coding:utf-8 -*-
# Filename: myQueue.py
# --------------------
# Function description:
# Queue of my own implementation
# --------------------
# Author: Dong Fuguo
# QQ: 306467355
# Email: dongfuguo2005@126.com
#--------------------
# Date: 2014-11-13, Updated on 2015-12-13
# --------------------

class myQueue:
    def __init__(self, size = 10):
        self._content = []
        self._size = size
        self._current = 0

    def setSize(self, size):
        if size < self._current:
            #如果缩小队列，应删除后面的元素
            for i in range(size, self._current)[::-1]:
                del self._content[i]
            self._current = size
        self._size = size

    def put(self, v):
        if self._current < self._size:
            self._content.append(v)
            self._current = self._current+1
        else:
            print('The queue is full')

    def get(self):
        if self._content:
            self._current = self._current-1
            return self._content.pop(0)
        else:
            print('The queue is empty')

    def show(self):
        if self._content:
            print(self._content)
        else:
            print('The queue is empty')
        
    def empty(self):
        self._content = []

    def isEmpty(self):
        if not self._content:
            return True
        else:
            return False

    def isFull(self):
        if self._current == self._size:
            return True
        else:
            return False

if __name__ == '__main__':
    print('Please use me as a module.')
```

### 自定义双端队列的用法

```javascript{.line-numbers}
>>> from myDeque import myDeque  #导入自定义双端队列类
>>> q = myDeque(range(5))               #创建双端队列对象
>>> q
myDeque([0, 1, 2, 3, 4], maxlen=10)
>>> q.appendLeft(-1)                          #在队列左侧入队
>>> q.appendRight(5)                         #在队列右侧入队
>>> q
myDeque([-1, 0, 1, 2, 3, 4, 5], maxlen=10)
>>> q.popLeft()                                   #在队列左侧出队
-1
>>> q.popRight()                                 #在队列右侧出队
5
>>> q.reverse()                     #元素翻转
>>> q
myDeque([4, 3, 2, 1, 0], maxlen=10)
>>> q.isEmpty()                     #测试队列是否为空
False
>>> q.rotate(-3)                      #元素循环左移
>>> q
myDeque([1, 0, 4, 3, 2], maxlen=10)
>>> q.setSize(20)                  #改变队列大小
>>> q
myDeque([1, 0, 4, 3, 2], maxlen=20)
>>> q.clear()                          #清空队列元素
>>> q
myDeque([], maxlen=20)
>>> q.isEmpty()
True
```

## 栈

* 栈是一种“后进先出（LIFO）”或“先进后出（FILO）”的数据结构。
* Python列表本身就可以实现栈结构的基本操作。例如，列表对象的append()方法是在列表尾部追加元素，类似于入栈操作；pop()方法默认是弹出并返回列表的最后一个元素，类似于出栈操作。
* 但是直接使用Python列表对象模拟栈操作并不是很方便，例如当列表为空时再执行pop()出栈操作时则会抛出一个不很友好的异常；另外，也无法限制栈的大小。

### 可以直接使用列表来实现栈结构

```javascript{.line-numbers}
>>> myStack = []
>>> myStack.append(3)
>>> myStack.append(5)
>>> myStack.append(7)
>>> myStack
[3, 5, 7]
>>> myStack.pop()
7
>>> myStack.pop()
5
>>> myStack.pop()
3
>>> myStack.pop()
出错
```

### 封装列表实现栈结构

```javascript{.line-numbers}
class Stack:
    def __init__(self, size = 10):
        self._content = []                 #使用列表存放栈的元素
        self._size = size                  #初始栈大小
        self._current = 0                  #栈中元素个数初始化为0
        
    def empty(self):
        self._content = []
        self._current = 0
        
    def isEmpty(self):
        if not self._content:
            return True
        else:
            return False
    def setSize(self, size):
        #如果缩小栈空间，则删除指定大小之后的已有元素
        if size < self._current:
            for i in range(size, self._current)[::-1]:
                del self._content[i]
            self._current = size
        self._size = size
    
    def isFull(self):
        if self._current == self._size:
            return True
        else:
            return False

                def push(self, v):
        if len(self._content) < self._size:
            self._content.append(v)
            self._current = self._current+1  #栈中元素个数加1
        else:
            print('Stack Full!')
            
    def pop(self):
        if self._content:
            self._current = self._current-1  #栈中元素个数减1
            return self._content.pop()
        else:
            print('Stack is empty!')
                def show(self):
        print(self._content)

    def showRemainderSpace(self):
        print('Stack can still PUSH ', self._size-self._current, ' elements.')

if __name__ == '__main__':
    print('Please use me as a module.')
```

### 自定义栈的用法

```javascript{.line-numbers}
>>> import Stack
>>> x = Stack.Stack()
>>> x.push(1)
>>> x.push(2)
>>> x.show()
[1, 2]
>>> x.pop()
2
>>> x.show()
[1]
>>> x.showRemainderSpace()
Stack can still PUSH  9  elements.
>>> x.isEmpty()
False
>>> x.isFull()
False
```

可直接使用列表来实现：

```javascript{.line-numbers}
>>> linkTable = []
>>> linkTable.append(3)
>>> linkTable.append(5)
>>> linkTable
[3, 5]
>>> linkTable.insert(1,4)
>>> linkTable
[3, 4, 5]
>>> linkTable.remove(linkTable[1])
>>> linkTable
[3, 5]
```
## 二叉树

使用代码中的类BinaryTree创建的对象不仅支持二叉树的创建以及前序遍历、中序遍历与后序遍历等三种常用的二叉树节点遍历方式，还支持二叉树中任意“子树”的遍历。

```javascript{.line-numbers}
class BinaryTree:
    def __init__(self, value):
        self.__left = None
        self.__right =  None
        self.__data = value
        
    def insertLeftChild(self, value):  #创建左子树
        if self.__left:
            print('__left child tree already exists.')
        else:
            self.__left = BinaryTree(value)
            return self.__left
                def insertRightChild(self, value): #创建右子树
        if self.__right:
            print('Right child tree already exists.')
        else:
            self.__right = BinaryTree(value)
            return self.__right
        
    def show(self):
        print(self.__data)

    def preOrder(self):                 #前序遍历
        print(self.__data)                #输出根节点的值
        if self.__left:
            self.__left.preOrder()      #遍历左子树
        if self.__right:
            self.__right.preOrder()    #遍历右子树

    def postOrder(self):                 #后序遍历
        if self.__left:
            self.__left.postOrder()
        if self.__right:
            self.__right.postOrder()
        print(self.__data)

    def inOrder(self):                 #中序遍历
        if self.__left:
            self.__left.inOrder()
        print(self.__data)
        if self.__right:
            self.__right.inOrder()

if __name__ == '__main__':
    print('Please use me as a module.')

```
自定义二叉树用法

```javascript{.line-numbers}
>>> import BinaryTree
>>> root = BinaryTree.BinaryTree('root')
>>> b = root.insertRightChild('B')
>>> a = root.insertLeftChild('A')
>>> c = a.insertLeftChild('C')
>>> d = c.insertRightChild('D')
>>> e = b.insertRightChild('E')
>>> f = e.insertLeftChild('F')
>>> root.inOrder()
C  D  A  root  B  F  E
>>> root.postOrder()
D  C  A  F  E  B  root
>>> b.inOrder()
B  F  E
```

## 有向图

```javascript{.line-numbers}
def searchPath(graph, start, end):
    results = []
    __generatePath(graph, [start], end, results)
    results.sort(key = lambda x:len(x))
    return results

def __generatePath(graph, path, end, results):
    current = path[-1]
    if current == end:
        results.append(path)
    else:
        for n in graph[current]:
            if n not in path:
                #path.append(n)
                __generatePath(graph, path + [n], end, results)

def showPath(results):
    print('The path from ',results[0][0], ' to ', results[0][-1], ' is:')
    for path in results:
        print(path)
        
if __name__ == '__main__':
    graph = {'A':['B', 'C', 'D'],
                   'B':['E'],
                   'C':['D', 'F'],
                   'D':['B', 'E', 'G'],
                   'E':['D'],
                   'F':['D', 'G'],
                   'G':['E']}
    r1 = searchPath(graph, 'A', 'D')
    showPath(r1)
    r2 = searchPath(graph, 'A', 'E')
    showPath(r2)
```



