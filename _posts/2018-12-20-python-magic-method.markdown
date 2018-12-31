---
layout: post
title: " Magic Method "
subtitle: "Python learning (3)"
author: "Bing Yan"
header-img: "img/magic/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Python
  - Learning
---
## ǰ��

&ensp;&ensp;&ensp;&ensp;ħ����������ͬ��������һ�����棬����������Ҫ��ʱ��Ϊ���ṩĳ�ַ�����������뷨ʵ�֡�ħ��������ָPython�ڲ��Ѿ������ģ���˫�»�������Χ�ķ�������Щ�����ڽ����ض��Ĳ���ʱ���Զ������ã�������Python����������ǻ۵Ľᾧ����Ϊ��ѧ�ߵ��ң�����Python��ħ������Ҳ�ͱ����Ϊ��Ҫ�������ѧϰһ�°ɡ�

## ����
### ʲô��ħ������(Magic Method)

&ensp;&ensp;&ensp;&ensp;�򵥵Ľ���python����˫�»��߿�ʼ�ͽ����ĺ����������Լ����壩Ϊħ��������<br/>
������ʵ�����Ķ���ķ���ʱ�Զ�����ħ���������о�����Ҫ��ʾ���õĺ������У���

### ΪʲôҪ��ħ������

ʹ��Python��ħ����������ʹPython�����ɶȱ�ø��ߣ�������Ҫ��дʱħ������Ҳ�����ڹ涨��Ĭ���������Ч������Ҫ��дʱҲ������ʹ���߸����Լ�����������д���ַ������ﵽ�Լ����ڴ�������������֪Python��֧��������������Python�Ļ���ħ��������ʹ��Python����Զ��������ø��á�


### ħ����������

���������Ӹ�ħ����������������լ
<br/>
![](/img/magic/mm-1.png)
<br/>
![](/img/magic/mm-2.png)
<br/>
![](/img/magic/mm-3.png)
<br/>
![](/img/magic/mm-4.png)
<br/>
![](/img/magic/mm-5.png)
<br/>
![](/img/magic/mm-6.png)
<br/>


### ����ħ������

��Ȼ����������˸���ħ�����������ǽ���������ѧϰ�������õ�ħ��������
<br/>

**ħ������__new__**

������__new__��������Ҫ�ǵ���̳�һЩ���ɱ��classʱ(����int, str, tuple)�� �ṩ����һ���Զ�����Щ���ʵ�������̵�;�������о���ʵ���Զ����metaclass������������Ҫһ����Զ�����������������ͣ�ͨ������int�����ǿ��ܻ�д�������Ĵ��롣

```
class PositiveInteger(int):

  def __init__(self, value):

    super(PositiveInteger, self).__init__(self, abs(value))

i = PositiveInteger(-3)

print i
```
<br/>
��������<br/>

```
-3
```
<br/>

���к�ᷢ�֣�������������������������������Ȼ�õ���-3��������Ϊ����int���ֲ��ɱ�Ķ�������ֻ����������__new__�����������Զ�������á�
<br/>
�޸Ĵ������£�
<br/>

```
class PositiveInteger(int):

  def __new__(cls, value):

    return super(PositiveInteger, cls).__new__(cls, abs(value))

i = PositiveInteger(-3)

print i
```
<br/>
��������<br/>

```
3
```
����������ʵ�ֵ���(singleton)����Ϊ��ÿһ��ʵ����������Ĺ��̶���ͨ��__new__�����Ƶģ�����ͨ������__new__���������� ���Ժܼ򵥵�ʵ�ֵ���ģʽ��
<br/>
```
class Singleton(object):

  def __new__(cls):

    # �ؼ������⣬ÿһ��ʵ������ʱ�����Ƕ�ֻ�᷵����ͬһ��instance����

    if not hasattr(cls, 'instance'):

      cls.instance = super(Singleton, cls).__new__(cls)

    return cls.instance

obj1 = Singleton()

obj2 = Singleton()

obj1.attr1 = 'value1'

print obj1.attr1, obj2.attr1

print obj1 is obj2
```

<br/>
��������<br/>

```
value1 value1
True
```

**ħ������__init__**

����֪��__init__�����������ĳ�ʼ����ϵͳִ�и÷���ǰ����ʵ�ö����Ѿ������ˣ�Ҫ��Ȼ��ʼ��ʲô�����أ�
����Ѵ����������ɽ���һ�����ӣ���ô__new__�������Դ�������ӵĹǼܣ���__init__���Ǹ�����װ�ޡ�<br/>
��ʵ__init__���������ش��ԭ������������һ��ԭ�����ڶ������������г�ʼ��������Ҫ��һ����ÿ�����������ȷ��ʼ������������������ڶ���ԭ����__init__()����ֵ�����ж�����ʽ��<br/>

����__init__()��__new__()��˳���������ͨ��������������֤��

```
class A:
 def __init__(self):
  print("__init__ ")
  print(self)
  super(A, self).__init__()
 
 def __new__(cls):
  print("__new__ ")
  print(self)
  return super(A, cls).__new__(cls)
 
 def __call__(self): # ���Զ����������
  print('__call__ ')
 
A()
```
������Ϊ��<br/>
```
__new__ 
<__main__.A object at 0x1007a95f8>
__init__ 
<__main__.A object at 0x1007a95f8>
```
<br/>
������������������__new__�����ȱ����ã�����һ��ʵ�����󣬽���__init__ �����á�<br/>
���ҿ���֪��__new__ �����ķ���ֵ�������ʵ���������ʵ������ᴫ�ݸ�__init__ �����ж����self�������Ա�ʵ��������Ա���ȷ�س�ʼ����<br/>

**ħ������__call__**

����__call__ ���������ò����ᵽһ��������ǿɵ��ö���callable��������ƽʱ�Զ���ĺ��������ú������඼���ڿɵ��ö��󣬵����ǿ��԰�һ������()Ӧ�õ�ĳ���������϶��ɳ�֮Ϊ�ɵ��ö����ж϶����Ƿ�Ϊ�ɵ��ö�������ú��� callable��<br/>
���������ʵ����__call__ ��������ôʵ������Ҳ����Ϊһ���ɵ��ö������ǻص��ʼ���Ǹ����ӣ�

```
class Foo(object): 
  def __call__(self): 
    pass
  
f = Foo()#��Foo��call 
f()#����f��call 
```

## �ܽ�
&ensp;&ensp;&ensp;&ensp;����ֻѧϰ��õ�����ħ����������__new__��__init__����__call__�ȷ������Ǳ���д�ģ���Ĭ�ϵ��ã�����Լ������ˣ�����override,����custom����Ȼoverride�ˣ�ͨ��Ҳ����ʽ���ý��в����Դﵽextend��Ŀ�ġ�<br/> 
&ensp;&ensp;&ensp;&ensp;֮��Ҳ�����Ŵ���Ļ��ۺ���Ŀ����Ҫ������ħ���������н�һ����ѧϰ��<br/> 

## �ο�����
�˴�ѧϰ��Ҫ���������漼����վ:<br/> 
https://www.jb51.net/article/118917.htm <br/>