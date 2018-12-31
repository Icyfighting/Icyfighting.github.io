---
layout: post
title: " Meta Class "
subtitle: "Python learning (2)"
author: "Bing Yan"
header-img: "img/metaclass/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Python
  - Learning
---
## ǰ��

&ensp;&ensp;&ensp;&ensp;����Ԫ����һ��ͨ���׶����ľ�����ı�����<br/>
����һ��һ����������������������<br/>

![](/img/metaclass/dao.jpg)
<br/>

*   �� ���� type
*   һ ���� metaclass(Ԫ�࣬���߽���������)
*   �� ���� class(�࣬���߽�ʵ��������)
*   �� ���� instance(ʵ��)
*   ���� ���� ʵ���ĸ��������뷽��������ƽ��ʹ��pythonʱ�����õľ������ǡ�

��һ�����ǽ���Ҫѧϰ���ص�--Ԫ��(Meta Class)��

## ����
### ʲô��Ԫ��(Meta Class)

&ensp;&ensp;&ensp;&ensp;�򵥵Ľ���Ԫ�ഴ����Python�����еĶ���<br/>
&ensp;&ensp;&ensp;&ensp;����˵Python��һ�ֶ�̬���ԣ�����̬���Ժ;�̬�������Ĳ�ͬ�����Ǻ������಻�Ǳ���ʱ����ģ���������ʱ��̬�����ġ�<br/>
&ensp;&ensp;&ensp;&ensp;class�Ķ���������ʱ��̬�����ģ�������class�ķ�������ʹ��type()������<br/>
&ensp;&ensp;&ensp;&ensp;ͨ��type()�������������ֱ��дclass����ȫһ���ģ���ΪPython����������class����ʱ��������ɨ��һ��class������﷨��Ȼ�����type()����������class��<br/>
&ensp;&ensp;&ensp;&ensp;����ʹ��type()��̬���������⣬Ҫ������Ĵ�����Ϊ��������ʹ��metaclass��ֱ��ΪԪ�ࡣ<br/>
&ensp;&ensp;&ensp;&ensp;�����Ƕ��������Ժ󣬾Ϳ��Ը�������ഴ����ʵ�������ԣ��ȶ����࣬Ȼ�󴴽�ʵ����������������봴�������أ��Ǿͱ������metaclass�������࣬���ԣ��ȶ���metaclass��Ȼ�󴴽��ࡣ���ԣ�metaclass�����㴴��������޸��ࡣ���仰˵������԰��࿴����metaclass���������ġ�ʵ������
<br/>

### ��̬������

������������������Ĵ�����ʽ
<br/>

*   ��������
*   type()����

**��������:**

```
def create_animal(type):
    if type == 'Dog':
        # ������
        class Dog(object):
            pass
 
        return Dog
    elif type == 'Cat':
        class Cat(object):
            pass
 
        return Cat
 
 
Dog = create_animal("Dog")
print(type(Dog))
dog = Dog()
print(type(dog))

```
<br/>
��������<br/>

```
<class 'type'>#������ <br/>
<class '__main__.create_animal.<locals>.Dog'>#��������
```
<br/>

����ͨ�����ú�����ͼ��ͬ�Ĳ�������������ͬ���࣬���������ص���������ã������Ƕ������ǿ���ͨ�����ص�������������
<br/>

**type()����:**

```
class Test1(object):
    pass
 
 
Test2 = type("Test2", (object,), {})
 
print(type(Test1))
print(type(Test2))
```
��������
<br/>
```
<class 'type'>
<class 'type'>
```

���Կ������ִ�����ʽ����ͬ��Ч����˵���������Ǵ��Ӧ�ö������ˣ�ԭ��type���Ǵ������һ��������python�����������࣬Ҳ����˵�����������Ԫ�࣬������pyhton���ǲ��ǻ���int��str...�ȵ����ͣ�int�������������������࣬��str�������������ַ������࣬�����typeҲ�ǣ�������python������������ࣨԪ�ࣩ��

<br/>


### �Զ���Ԫ��

�Զ�����ĵ�Ŀ�ģ�����������Ĵ�����Ȼ���޸�һЩ���ԣ�Ȼ�󷵻ظ��ࡣ�о���װ�����ɵ����飬ֻ��װ����������һ��������ͬ����һ��������ȥ��Ȼ�󱻶������һЩ��������󱻷��ء�

```
def upper_attr(class_name, class_parents, class_attr):
    """
    ����һ������,�����Զ���Ϊ��д����ʽ
    :param class_name:  �������
    :param class_parents: ��ĸ���tuple
    :param class_attr: ��Ĳ���
    :return: ������
    """
    # ������һ��generator
    attrs = ((name, value) for name, value in class_attr.items() if not name.startswith('__'))
    uppercase_attrs = dict((name.upper(), value) for name, value in attrs)
    return type(class_name, class_parents, uppercase_attrs)

__metaclass__ = upper_attr

pw = upper_attr('Trick', (), {'bar': 0})
print hasattr(pw, 'bar')
print hasattr(pw, 'BAR')
print pw.BAR
```

��������<br/>
>False<br/>
True

���Դ����濴����ʵ����һ��Ԫ��(metaclass)�� Ȼ��ָ����ģ��ʹ�����Ԫ���������࣬���Ե�����ʹ��type�����ഴ����ʱ�򣬿��Է���Сд��bar�������滻���˴�д��BAR����������������������������Բ�����ӡ������<br/>

## �ܽ�
&ensp;&ensp;&ensp;&ensp;����ʵ���ܹ���������ʵ���Ķ��󡣺ðɣ���ʵ�ϣ��౾��Ҳ��ʵ������Ȼ��������Ԫ���ʵ����<br/>
&ensp;&ensp;&ensp;&ensp;Python�е�һ�ж��Ƕ�������Ҫô�����ʵ����Ҫô��Ԫ���ʵ��������type��typeʵ���������Լ���Ԫ�࣬�ڴ�Python��������ɲ������ܹ������ģ�����ͨ����ʵ�ֲ���ˣһЩС�ֶ������ġ���Σ�Ԫ���Ǻܸ��ӵġ����ڷǳ��򵥵��࣬����ܲ�ϣ��ͨ��ʹ��Ԫ�����������޸ġ�

## �ο�����
�˴�ѧϰ��Ҫ���������漼����վ:<br/> 
https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python <br/>
http://blog.jobbole.com/21351/ <br/>