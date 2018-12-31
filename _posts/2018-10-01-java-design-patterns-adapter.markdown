---
layout: post
title: "Design Patterns (4)"
subtitle: "Design patterns -- Adapter "
author: "Bing Yan"
header-img: "img/dp-adapter/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Java
  - Design Patterns
  - Learning
---
## ǰ��

�����ϼ��ε����ģʽ������ѧϰ���Ѿ��˽������ģʽ������ͻ���ԭ��<br/>
�����ѧϰ��ʼ����Ҫ���20���־�������ģʽ�����壬�������;���ʵ��������ѧϰ��<br/>
��Щѧϰ�����ݣ����Ǹ��������϶������ģʽ���鼮�����͵����ݽ�������<br/>
����ѧϰ������(Adapter)ģʽ��

## ����
### ʲô��������(Adapter)ģʽ

����ʵ�����У�������������������ӿڲ����ݶ�������һ������ʵ������ʱ��Ҫ�����߽������䡣���磬�����ĵ���ͬ��Ӣ�ĵ��˶Ի�ʱ��Ҫһ�����룬��ֱ����ıʼǱ����Խӽ�����Դʱ��Ҫһ����Դ���������ü��������������� SD �ڴ濨ʱ��Ҫһ���������ȡ�<br/>
����������Ҳ���ܳ��֣���Ҫ�����ľ���ĳ��ҵ���ܵ���������е���������Ѿ����ڣ��������뵱ǰϵͳ�Ľӿڹ淶�����ݣ�������¿�����Щ����ɱ��ֺܸߣ���ʱ��������ģʽ�ܺܺõؽ����Щ���⡣<br/>
��һ����Ľӿ�ת���ɿͻ�ϣ��������һ���ӿڣ�ʹ��ԭ�����ڽӿڲ����ݶ�����һ��������Щ����һ������������ģʽ��Ϊ��ṹ��ģʽ�Ͷ���ṹ��ģʽ���֣�ǰ����֮�����϶ȱȺ��߸ߣ���Ҫ�����Ա�˽�����������е����������ڲ��ṹ������Ӧ����Խ���Щ��<br/>

### ������ģʽ�ص�
<br/>
�ŵ㣺 <br/>

*   �ͻ���ͨ������������͸���ص���Ŀ��ӿڡ�
*   �������ִ���࣬����Ա����Ҫ�޸�ԭ�д�����������е��������ࡣ
*   ��Ŀ��������������������Ŀ�������������ӿڲ�һ�µ����⡣
<br/>
ȱ�㣺 <br/>

*   ������������˵��������������ʵ�ֹ��̱Ƚϸ��ӡ�

<br/>

### ������ģʽ�Ľṹ

<br/>
������ģʽ����Ҫ�أ�<br/>

*   Ŀ�꣨Target���ӿ�: ��ǰϵͳҵ�����ڴ��Ľӿڣ��������ǳ������ӿڡ�
*   �����ߣ�Adaptee����: ���Ǳ����ʺ�������ִ�������е�����ӿڡ�
*   ��������Adapter����: ����һ��ת������ͨ���̳л����������ߵĶ��󣬰������߽ӿ�ת����Ŀ��ӿڣ��ÿͻ���Ŀ��ӿڵĸ�ʽ���������ߡ�

<br/>
��������ģʽ�Ľṹͼ����ͼ��ʾ: <br/>

![](/img/dp-adapter/adapter-1.png)

<br/>
����������ģʽ�Ľṹͼ����ͼ��ʾ: <br/>

![](/img/dp-adapter/adapter-2.png)

### ������ģʽ��ʵ��
<br/>
��ʵ�ַ�ʽ��Ҫ�����֣�<br/>
1. ���������(���ü̳�ʵ��) <br/>
2. ����������(���ö�����Ϸ�ʽʵ��) <br/>

*   ��������ģʽ�Ĵ������£�<br/>

```
package adapter;
//Ŀ��ӿ�
interface Target
{
    public void request();
}
//�����߽ӿ�
class Adaptee
{
    public void specificRequest()
    {       
        System.out.println("�������е�ҵ����뱻���ã�");
    }
}
//����������
class ClassAdapter extends Adaptee implements Target
{
    public void request()
    {
        specificRequest();
    }
}
//�ͻ��˴���
public class ClassAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("��������ģʽ���ԣ�");
        Target target = new ClassAdapter();
        target.request();
    }
}
```
��������н�����£�<br/>
>��������ģʽ���ԣ�<br/>
�������е�ҵ����뱻���ã�

*   ����������ģʽ�Ĵ�������:<br/>

```
package adapter;
//������������
class ObjectAdapter implements Target
{
    private Adaptee adaptee;
    public ObjectAdapter(Adaptee adaptee)
    {
        this.adaptee=adaptee;
    }
    public void request()
    {
        adaptee.specificRequest();
    }
}
//�ͻ��˴���
public class ObjectAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("����������ģʽ���ԣ�");
        Adaptee adaptee = new Adaptee();
        Target target = new ObjectAdapter(adaptee);
        target.request();
    }
}
```

˵��������������ģʽ�еġ�Ŀ��ӿڡ��͡��������ࡱ�Ĵ���ͬ��������ģʽһ����ֻҪ�޸���������Ϳͻ��˵Ĵ��뼴�ɡ�
<br/>
��������н�����£�<br/>
>����������ģʽ���ԣ�<br/>
�������е�ҵ����뱻���ã�<br/>

### ģʽ��Ӧ�ó���

������ģʽ��Adapter��ͨ�����������³���:<br/>

*   ��ǰ������ϵͳ����������ϵͳ����������࣬����ӿ�ͬ��ϵͳ�Ľӿڲ�һ�¡�
*   ʹ�õ������ṩ�������������ӿڶ�����Լ�Ҫ��Ľӿڶ��岻ͬ��

### ģʽ����չ

������ģʽ��Adapter������չΪ˫��������ģʽ��˫����������ȿ��԰������߽ӿ�ת����Ŀ��ӿڣ�Ҳ���԰�Ŀ��ӿ�ת���������߽ӿڣ���ṹͼ��ͼ��ʾ��<br/> 
![](/img/dp-adapter/adapter-3.png)
<br/>
```
package adapter;
//Ŀ��ӿ�
interface TwoWayTarget
{
    public void request();
}
//�����߽ӿ�
interface TwoWayAdaptee
{
    public void specificRequest();
}
//Ŀ��ʵ��
class TargetRealize implements TwoWayTarget
{
    public void request()
    {       
        System.out.println("Ŀ����뱻���ã�");
    }
}
//������ʵ��
class AdapteeRealize implements TwoWayAdaptee
{
    public void specificRequest()
    {       
        System.out.println("�����ߴ��뱻���ã�");
    }
}
//˫��������
class TwoWayAdapter  implements TwoWayTarget,TwoWayAdaptee
{
    private TwoWayTarget target;
    private TwoWayAdaptee adaptee;
    public TwoWayAdapter(TwoWayTarget target)
    {
        this.target=target;
    }
    public TwoWayAdapter(TwoWayAdaptee adaptee)
    {
        this.adaptee=adaptee;
    }
    public void request()
    {
        adaptee.specificRequest();
    }
    public void specificRequest()
    {       
        target.request();
    }
}
//�ͻ��˴���
public class TwoWayAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("Ŀ��ͨ��˫�����������������ߣ�");
        TwoWayAdaptee adaptee=new AdapteeRealize();
        TwoWayTarget target=new TwoWayAdapter(adaptee);
        target.request();
        System.out.println("-------------------");
        System.out.println("������ͨ��˫������������Ŀ�꣺");
        target=new TargetRealize();
        adaptee=new TwoWayAdapter(target);
        adaptee.specificRequest();
    }
}
```
��������н�����£�<br/>
>Ŀ��ͨ��˫�����������������ߣ�<br/>
�����ߴ��뱻���ã�<br/>
-------------------<br/>
������ͨ��˫������������Ŀ�꣺<br/>
Ŀ����뱻���ã�

## �ܽ�

&ensp;&ensp;&ensp;&ensp;������ģʽҲ��һ�ְ�װģʽ����֮ǰ�� Decorator װ��ģʽͬ�����а�װ�Ĺ��ܣ����⣬����������ģʽ��������ʽί�е���˼�����棨��ʵ��������Ҳ��������˼��ֻ�����Ƚ��������ѣ�����ô������Ϊ���� Proxy ����ģʽҲ�е����ơ�<br/>

&ensp;&ensp;&ensp;&ensp;������һ��Ա������� Decorator �� Proxy�� Adapter ��ʵ�������������ҪĿ�ģ�����ÿ�����ģʽ�����������������֮�⣬�������ڰ�װ��ǰ����ж���ġ�����Ĺ����ϵ���������Ϊ����Ϊ���Ƕ���ί�е�ʵ����˼�����档<br/>

&ensp;&ensp;&ensp;&ensp;Ҳ������˵������ģʽ���ʺ�����ϸ��ƽ׶�ʹ����������һ�ֲ���ģʽ��ר������ϵͳ������չ���޸�ʱ���á�

## �ο�����
�˴�ѧϰ��Ҫ���������漼����վ:<br/> 
http://c.biancheng.net/view/1361.html <br/>
https://www.cnblogs.com/V1haoge/p/6479118.html <br/>
