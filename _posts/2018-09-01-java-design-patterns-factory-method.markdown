---
layout: post
title: "Design Patterns (3)"
subtitle: "Design patterns -- Factory Method "
author: "Bing Yan"
header-img: "img/dp_factory/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Java
  - Design Patterns
  - Learning
---
## ǰ��

���������ε����ģʽ������ѧϰ���Ѿ��˽������ģʽ������ͻ���ԭ��<br/>
�����ѧϰ��ʼ����Ҫ���20���־�������ģʽ�����壬�������;���ʵ��������ѧϰ��<br/>
��Щѧϰ�����ݣ����Ǹ��������϶������ģʽ���鼮�����͵����ݽ�������<br/>
����ѧϰ��������(Factory Method)ģʽ��

## ����
### ʲô�ǹ�������(Factory Method)

����һ��������Ʒ����Ĺ����ӿڣ�����Ʒ�����ʵ�ʴ��������Ƴٵ������ӹ����൱�С������㴴����ģʽ����Ҫ��ġ�������ʹ������롱���ص㡣<br/>
���ǰѱ������Ķ����Ϊ����Ʒ�����Ѵ�����Ʒ�Ķ����Ϊ�������������Ҫ�����Ĳ�Ʒ���ֻ࣬Ҫһ��������Ϳ�����ɣ�����ģʽ�С��򵥹���ģʽ������������ GoF �� 23 �־������ģʽ������ȱ���������²�Ʒʱ��Υ��������ԭ�򡱡�<br/>
����ѧϰ�ġ���������ģʽ���ǶԼ򵥹���ģʽ�Ľ�һ�����󻯣���ô��ǿ���ʹϵͳ�ڲ��޸�ԭ�����������������µĲ�Ʒ�������㿪��ԭ��<br/>

### ��������ģʽ�ص�
<br/>
�ŵ㣺 <br/>

*   �û�ֻ��Ҫ֪�����幤�������ƾͿɵõ���Ҫ�Ĳ�Ʒ������֪����Ʒ�ľ��崴������
*   ��ϵͳ�����µĲ�Ʒʱֻ��Ҫ��Ӿ����Ʒ��Ͷ�Ӧ�ľ��幤���࣬�����ԭ���������κ��޸ģ����㿪��ԭ��

ȱ�㣺 <br/>
*   ÿ����һ����Ʒ��Ҫ����һ�������Ʒ���һ����Ӧ�ľ��幤���࣬��������ϵͳ�ĸ��Ӷȡ�

<br/>

### ����ģʽ�Ľṹ

<br/>
��������ģʽ����Ҫ�أ�<br/>

*   ���󹤳� (Abstract Factory): �ṩ�˴�����Ʒ�Ľӿڣ�������ͨ�������ʾ��幤���Ĺ������� newProduct() ��������Ʒ��
*   ���幤�� (Concrete Factory): ��Ҫ��ʵ�ֳ��󹤳��еĳ��󷽷�����ɾ����Ʒ�Ĵ�����
*   �����Ʒ (Product): �����˲�Ʒ�Ĺ淶�������˲�Ʒ����Ҫ���Ժ͹��ܡ�
*   �����Ʒ (Concrete Product): ʵ���˳����Ʒ��ɫ������Ľӿڣ��ɾ��幤������������ͬ���幤��֮��һһ��Ӧ��

<br/>
��ṹ����ͼ��ʾ: <br/>

![](/img/dp_factory/factory-1.png)

<br/>

### ��������ģʽ��ʵ��
<br/>
���������ṹͼ��д����ģʽ�Ĵ������£�<br/>

```
package FactoryMethod;
public class AbstractFactoryTest
{
    public static void main(String[] args)
    {
        try
        {
            Product a;
            AbstractFactory af;
            af=(AbstractFactory) ReadXML1.getObject();
            a=af.newProduct();
            a.show();
        }
        catch(Exception e)
        {
            System.out.println(e.getMessage());
        }
    }
}
//�����Ʒ���ṩ�˲�Ʒ�Ľӿ�
interface Product
{
    public void show();
}
//�����Ʒ1��ʵ�ֳ����Ʒ�еĳ��󷽷�
class ConcreteProduct1 implements Product
{
    public void show()
    {
        System.out.println("�����Ʒ1��ʾ...");
    }
}
//�����Ʒ2��ʵ�ֳ����Ʒ�еĳ��󷽷�
class ConcreteProduct2 implements Product
{
    public void show()
    {
        System.out.println("�����Ʒ2��ʾ...");
    }
}
//���󹤳����ṩ�˳�Ʒ�����ɷ���
interface AbstractFactory
{
    public Product newProduct();
}
//���幤��1��ʵ���˳�Ʒ�����ɷ���
class ConcreteFactory1 implements AbstractFactory
{
    public Product newProduct()
    {
        System.out.println("���幤��1����-->�����Ʒ1...");
        return new ConcreteProduct1();
    }
}
//���幤��2��ʵ���˳�Ʒ�����ɷ���
class ConcreteFactory2 implements AbstractFactory
{
    public Product newProduct()
    {
        System.out.println("���幤��2����-->�����Ʒ2...");
        return new ConcreteProduct2();
    }
}
```

```
package FactoryMethod;
import javax.xml.parsers.*;
import org.w3c.dom.*;
import java.io.*;
class ReadXML1
{
    //�÷������ڴ�XML�����ļ�����ȡ������������������һ��ʵ������
    public static Object getObject()
    {
        try
        {
            //�����ĵ�����
            DocumentBuilderFactory dFactory=DocumentBuilderFactory.newInstance();
            DocumentBuilder builder=dFactory.newDocumentBuilder();
            Document doc;                           
            doc=builder.parse(new File("src/FactoryMethod/config1.xml"));        
            //��ȡ�����������ı��ڵ�
            NodeList nl=doc.getElementsByTagName("className");
            Node classNode=nl.item(0).getFirstChild();
            String cName="FactoryMethod."+classNode.getNodeValue();
            //System.out.println("��������"+cName);
            //ͨ����������ʵ�����󲢽��䷵��
            Class<?> c=Class.forName(cName);
              Object obj=c.newInstance();
            return obj;
         }  
         catch(Exception e)
         {
                   e.printStackTrace();
                   return null;
         }
    }
}

```

���Ը���XML�����ļ�ָ����Ҫʹ�õľ��幤��<br/>

```
<?xml version="1.0" encoding="UTF-8"?>
<config>
  <className>ConcreteFactory1</className>
</config>
```
���н�����£�<br/>
>���幤��1����-->�����Ʒ1... <br/>
�����Ʒ1��ʾ...

��XML�����ļ��е�ConcreteFactory1 ��Ϊ ConcreteFactory2����������н�����£�<br/>
>���幤��2����-->�����Ʒ2... <br/>
�����Ʒ2��ʾ...

### ģʽ��Ӧ�ó���

��������ģʽͨ�����������³���:<br/>
*   �ͻ�ֻ֪��������Ʒ�Ĺ�����������֪������Ĳ�Ʒ������ TCL ���ӹ��������ŵ��ӹ����ȡ�
*   ��������������ɶ�������ӹ����е�ĳһ����ɣ������󹤳�ֻ�ṩ������Ʒ�Ľӿڡ�
*   �ͻ������Ĵ�����Ʒ��ϸ�ڣ�ֻ���Ĳ�Ʒ��Ʒ�ơ�

### ģʽ����չ

����Ҫ���ɵĲ�Ʒ�����Ҳ������ӣ�һ�����幤����Ϳ����������ʱ����ɾ�����󹤳��ࡣ��ʱ��������ģʽ���˻����򵥹���ģʽ����ṹͼ��ͼ��ʾ: <br/>

![](/img/dp_factory/factory-2.png)
<br/>

## �ܽ�

&ensp;&ensp;����ʵ���������ֹ�Խ��Խϸ��Խ��Խרҵ�������ֲ�Ʒ��ר�ŵĹ������������׸�����Ը������Сũ����ʱ�������������˲�Ʒ���������ڣ����������Ч�ʡ�<br/>   �ڳ�������У���������ģʽҲ�ṩ��һ��������˼·��ʵ������������������ʹ������롣<br/>   
&ensp;&ensp;�����Ǽ򵥹���ģʽ����������ģʽ�����ǳ��󹤳�ģʽ�����Ƕ����ڹ���ģʽ������ʽ���ص���Ҳ�Ǽ�Ϊ���Ƶģ����ǵ�����Ŀ�Ķ���Ϊ�˽����ʹ��ʱ�����ǲ���ȥ�������ģʽ���׹�������ģʽ���ǳ��󹤳�ģʽ����Ϊ����֮����ݱ䳣����������ĥ��͸�ġ�<br/>  &ensp;&ensp;������ᷢ�֣�����ʹ�õĹ�������ģʽ�������������٣��Լ��޸ģ�������һ���·������������еĲ�Ʒ�����˲�ͬ�ȼ��ṹ�еĲ�Ʒ�壬���ͱ�ɳ��󹤳�ģʽ�ˣ������ڳ��󹤳�ģʽ��������һ������ʹ���ṩ�Ĳ�Ʒ���ٹ��ɲ�Ʒ��֮�������ݱ���˹�������ģʽ��<br/>   
&ensp;&ensp;���ԣ���ʹ�ù���ģʽʱ��ֻ��Ҫ���Ľ�����϶ȵ�Ŀ���Ƿ�ﵽ�ˡ�

## Reference-1
�˴�ѧϰ��Ҫ���������漼����վ:<br/> 
http://c.biancheng.net/view/1348.html <br/>
https://www.cnblogs.com/yumo1627129/p/7197524.html <br/>
