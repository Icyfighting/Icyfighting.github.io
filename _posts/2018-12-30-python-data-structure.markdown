---
layout: post
title: " Python Data Structure learning"
subtitle: "List & Tuple & Set & Dictionary"
author: "Bing Yan"
header-img: "img/magic/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Python
  - Data Structure
  - Learning
---
## ǰ��



## ����
### �б�(List)

&ensp;&ensp;&ensp;&ensp;������Python������������ݽṹ�������е�ÿ��Ԫ�ض�����һ������ - ����λ�ã�����������һ��������0���ڶ���������1���������ơ�<br/>
&ensp;&ensp;&ensp;&ensp;Python��6�����е��������ͣ�����������б��Ԫ�顣<br/>
&ensp;&ensp;&ensp;&ensp;���ж����Խ��еĲ���������������Ƭ���ӣ��ˣ�����Ա��<br/>
&ensp;&ensp;&ensp;&ensp;���⣬Python�Ѿ�����ȷ�����еĳ����Լ�ȷ��������С��Ԫ�صķ�����<br/>
&ensp;&ensp;&ensp;&ensp;�б�����õ�Python�������ͣ���������Ϊһ���������ڵĶ��ŷָ�ֵ���֡�<br/>
&ensp;&ensp;&ensp;&ensp;�б���������Ҫ������ͬ�����͡�<br/>


**List����**
����һ���б�ֻҪ�Ѷ��ŷָ��Ĳ�ͬ��������ʹ�÷��������������ɡ�<br/>

```
list1 = ['physics', 'chemistry', 1997, 2000]
list2 = [1, 2, 3, 4, 5 ]
list3 = ["a", "b", "c", "d"]
```
**List��ֵ�ķ���**
ʹ���±������������б��е�ֵ��ͬ����Ҳ����ʹ�÷����ŵ���ʽ��ȡ�ַ���<br/>

```
list1 = ['physics', 'chemistry', 1997, 2000]
list2 = [1, 2, 3, 4, 5, 6, 7 ]
print("list1[0]: ", list1[0])
print(list2[1:5]: ", list2[1:5])
```
<br/>
��������<br/>

```
list1[0]:  physics
list2[1:5]:  [2, 3, 4, 5]
```

**����List**
```
list = []          ## ���б�
list.append('Google')   ## ʹ�� append() ���Ԫ��
list.append('Runoob')
print(list)
```
<br/>
��������<br/>

```
['Google', 'Runoob']
```

**ɾ��List��Ԫ��**

```
list1 = ['physics', 'chemistry', 1997, 2000]
 
print(list1)
del(list1[2])
print("After deleting value at index 2 : ")
print(list1)
```
<br/>
��������<br/>

```
['physics', 'chemistry', 1997, 2000]
After deleting value at index 2 :
['physics', 'chemistry', 2000]
```

### Ԫ��(Tuple)

Python��Ԫ�����б����ƣ���֮ͬ������Ԫ���Ԫ�ز����޸ġ�<br/>
Ԫ��ʹ��С���ţ��б�ʹ�÷����š�

**Tuple����**

Ԫ�鴴���ܼ򵥣�ֻ��Ҫ�����������Ԫ�أ���ʹ�ö��Ÿ������ɣ�<br/>
ע�⣺Ԫ����ֻ����һ��Ԫ��ʱ����Ҫ��Ԫ�غ�����Ӷ��š�<br/>

```
tup1 = ('physics', 'chemistry', 1997, 2000)
tup2 = (1, 2, 3, 4, 5 )
tup3 = "a", "b", "c", "d"
tup4 = (50,)
```
<br/>

**Tuple����**

```
tup1 = ('physics', 'chemistry', 1997, 2000)
tup2 = (1, 2, 3, 4, 5, 6, 7 )
 
print("tup1[0]: ", tup1[0])
print("tup2[1:5]: ", tup2[1:5])
```
<br/>
��������<br/>

```
tup1[0]:  physics
tup2[1:5]:  (2, 3, 4, 5)
```

**Tuple�޸�**

Ԫ���е�Ԫ��ֵ�ǲ������޸ĵģ������ǿ��Զ�Ԫ�����������ϣ�<br/>

```
tup1 = (12, 34.56)
tup2 = ('abc', 'xyz')
 
# tup1[0] = 100   #�޸�Ԫ��Ԫ�ز����ǷǷ���
 
# ����һ���µ�Ԫ��
tup3 = tup1 + tup2
print(tup3)
```
<br/>
��������<br/>

```
(12, 34.56, 'abc', 'xyz')
```

**Tupleɾ��**

Ԫ���е�Ԫ��ֵ�ǲ�����ɾ���ģ������ǿ���ʹ��del�����ɾ������Ԫ��:
```
tup = ('physics', 'chemistry', 1997, 2000)
 
print(tup)
del(tup)
print("After deleting tup : ")
print(tup)
```
<br/>
��������<br/>

```
('physics', 'chemistry', 1997, 2000)
After deleting tup :
Traceback (most recent call last):
  File "test.py", line 9, in <module>
    print tup
NameError: name 'tup' is not defined
```

### ����(Set)

���ϣ�set����һ������Ĳ��ظ�Ԫ�����С�

**Set����**
����ʹ�ô����� { } ���� set() �����������ϣ�ע�⣺����һ���ռ��ϱ����� set() ������ { }����Ϊ { } ����������һ�����ֵ䡣:
>parame = {value01,value02,...} <br/>
����set(value)<br/>

```
>>>basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # ������ʾ����ȥ�ع���
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # �����ж�Ԫ���Ƿ��ڼ�����
True
>>> 'crabgrass' in basket
False
>>>a = {x for x in 'abracadabra' if x not in 'abc'}  #�����Ƶ�ʽ(Set comprehension)
>>> a
{'r', 'd'}
```

**SetԪ���Ƴ�**

```
>>>thisset = set(("Google", "Runoob", "Taobao"))
>>> thisset.remove("Taobao")
>>> print(thisset)
{'Google', 'Runoob'}
>>> thisset.remove("Facebook")   # ʹ��remove()�����ڻᷢ������
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'Facebook'
```

�Ƽ�ʹ��discard()��Ԫ�ز�����ʱ�����ᷢ������<br/>

```
>>>thisset = set(("Google", "Runoob", "Taobao"))
>>> thisset.discard("Facebook")  # �����ڲ��ᷢ������
>>> print(thisset)
{'Taobao', 'Google', 'Runoob'}
```

���ɾ�������е�һ��Ԫ��<br/>
Ȼ���ڽ���ģʽ��pop ��ɾ�����ϵĵ�һ��Ԫ�أ������ļ��ϵĵ�һ��Ԫ�أ�<br/>

```
thisset = set(("Google", "Runoob", "Taobao", "Facebook"))
x = thisset.pop()
print(x)
```
<br/>
��������<br/>

```
Runoob
```

Ҳ������ռ���<br/>

```
>>>thisset = set(("Google", "Runoob", "Taobao"))
>>> thisset.clear()
>>> print(thisset)
set()
```

**SetԪ�ظ�������**

```
>>>thisset = set(("Google", "Runoob", "Taobao"))
>>> len(thisset)
3
```


**SetԪ���Ƿ����**

�ж�Ԫ�� x �Ƿ��ڼ��� s �У����ڷ��� True�������ڷ��� False��<br/>

```
>>>thisset = set(("Google", "Runoob", "Taobao"))
>>> "Runoob" in thisset
True
>>> "Facebook" in thisset
False
```

### �ֵ�(Dictionary)

�ֵ�����һ�ֿɱ�����ģ�ͣ��ҿɴ洢�������Ͷ���<br/>

**Dictionary����**

�ֵ��ÿ����ֵ key=>value ����ð�� : �ָÿ����ֵ��֮���ö��� , �ָ�����ֵ�����ڻ����� {} �У�<br/>
d = {key1 : value1, key2 : value2 } <br/>
��һ����Ψһ�ģ�����ظ�����һ����ֵ�Ի��滻ǰ��ģ�ֵ����ҪΨһ��<br/>
ֵ����ȡ�κ��������ͣ����������ǲ��ɱ�ģ����ַ��������ֻ�Ԫ�顣<br/>
*ѧϰ�ʼǣ�<br/>

����ֵ����Ҫ�󣬻��и�׼ȷ��˵���ǣ�<br/>
>python��ʲô��������Ϊ�ֵ��key����__hash__�����������ֵ��key��û��������Ϊ�ֵ��key;<br/>
����list��dict��set���ڲ����ٴ���������������֮һ��tuple֮�⣬������������Ϊ�ֵ��key��

```
>>>dict = {'a': 1, 'b': 2, 'b': '3'}
>>> dict['b']
'3'
>>> dict
{'a': 1, 'b': '3'}
```

**Dictionary����**

����Ӧ�ļ����뷽������
```
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
print("dict['Name']: ", dict['Name'])
print("dict['Age']: ", dict['Age'])
```
<br/>
��������<br/>

```
dict['Name']:  Zara
dict['Age']:  7
```

������ֵ���û�еļ��������ݣ�������������£�<br/>

```
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
print("dict['Alice']: ", dict['Alice'])
```
<br/>
��������<br/>
```
dict['Alice']: 
Traceback (most recent call last):
  File "test.py", line 5, in <module>
    print "dict['Alice']: ", dict['Alice']
KeyError: 'Alice'
```

Ϊ�˱��������쳣������ʹ��collections.defaultdict()����������Ĭ��ֵ��dictionary��<br/>
```
from collections import defaultdict
d2 = defaultdict(lambda :'default value')
d2['one'] = 1
d2['two'] = 2
print(d2['two'])
print(d2['three'])
```
<br/>
��������<br/>
```
2
default value
```

**Dictionary�޸�**

���ֵ���������ݵķ����������µļ�/ֵ�ԣ��޸Ļ�ɾ�����м�/ֵ��:<br/>
```
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
dict['Age'] = 8 # ����
dict['School'] = "RUNOOB" # ��� 
print("dict['Age']: ", dict['Age'])
print("dict['School']: ", dict['School'])
```
<br/>
��������<br/>

```
dict['Age']:  8
dict['School']:  RUNOOB
```

**Dictionaryɾ��**

*   ɾ���ֵ�Ԫ��
*   ɾ���ֵ�

```
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
 
del dict['Name']  # ɾ������'Name'����Ŀ
dict.clear()      # ��մʵ�������Ŀ
del dict          # ɾ���ʵ�
```


## �ܽ�
&ensp;&ensp;&ensp;&ensp;����ѧϰ��Python�г��õ�4�����ݽṹ�������в�ͬ�Ĵ洢�ṹ���ص㡣���˼�¼�ļ��ֳ��õĴ��������ʡ��޸ġ�ɾ���Ȼ���������ÿһ�����ݽṹ���໹�ṩ�˷ḻ�ķ��������������<br/>
&ensp;&ensp;&ensp;&ensp;�ڱ�д����Ĺ����У�Ҳ�Ѿ�ʹ�õ���һ���֣�����Ҫ������Ҫʹ��ʲô����ʱ��ʹ��help���鿴����ķ���˵�������Ա��ñ�ѧ��

## �ο�����
�˴�ѧϰ��Ҫ���������漼����վ:<br/> 
http://www.runoob.com/python3/python3-tutorial.html <br/>