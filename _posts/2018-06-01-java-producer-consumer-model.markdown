---
layout: post
title: "Producer-Consumer model"
subtitle: "KFC vs McDonald's "
author: "Bing Yan"
header-img: "img/deadlock/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Java
  - Learning
---
## ǰ��
���Ŷ����˶������ϵ»����������ѣ����߽������ѵ�ʱ�������ǵĵ㵥���̺Ͳ���ģ��ʮ�ֽӽ�����Ȼÿ�ҵ�������������죬���Ǵ�ž�ֻ������ģ�͡��ڿϵ»����㵥֮��㵥Ա��������ʳ����ɷ�װ֮����������ǰ��Ȼ��������ˣ���ʱ����Щ��ʱ����û��ɾͻ�����һ����̨���Ժ��������������͵ĵ��ģ�ʹ����ǣ��������֮��Ҫ����������������֮����һλ��ͣ���ȡ�͵������Աߵȴ�����һ������Աר������͡�

KFC��<br/>
![](/img/producer/KFC.png)

McDonald's��<br/>
![](/img/producer/McDonald.png)

�ڲ���ģ���У��ϵ»��Ƚ�������һ���̰߳����еķ������꣬�����������ڷ����������Ǹ�רע���Լ���ҵ�񡣶��ϵ»���ģ����BIO��������ģ��������ƣ����͵�ģ������������������ģ��ʮ�����ơ�<br/>
<br/>
���ڴ��͵�����վ�У����ǵķ������Ӧ�ý���֮����ͨ����Ϣ�����ڱ˴˼�ͨ�ŵġ���Ϣ���к�Ӧ��֮��ļܹ���ϵ����������������ģ�͡�

## ����
### ������������ģ��(Producer-Consumer model)

������������ģ�;���������������һ��ϵͳ�У����������ߺ����������ֽ�ɫ������ͨ���ڴ滺��������ͨ�ţ�������������������Ҫ�����ϣ������߰��������ɲ�Ʒ������������ģʽ����ͼ:

![](/img/producer/model.png)

�����淢չ�ķ��������У�Ʃ��ע���û����ַ��������ܽ���ɺü��ֶ����ķ����˺���֤��������֤�룬�ֻ�������ȣ���������Ϊ�����ߣ��ȴ��û��������ݣ���ǰ̨�����ύ֮��ᾭ���ֽⲢ���͵������������ڵ�url���ַ����Ǹ���ɫ���൱�������ߡ��������ڻ�ȡ����ʱ���п���һ�β��ܴ����꣬��ô���Ǹ�����һ��������У��Ǿ����ڴ滺�����ˡ���������Ŀ�ܽ�����Ϣ���С�

### ������������ģ�͵�ʵ��
**5��ʵ�ַ���**

*   ��synchronized�Դ洢������Ȼ����objectԭ����wait() �� notify()��ͬ��
*   ��concurrent.locks.Lock��Ȼ����condition��await() ��signal()��ͬ��
*   ֱ��ʹ��concurrent.BlockingQueue
*   ʹ��PipedInputStream/PipedOutputStream
*   ʹ���ź���semaphore


**synchronizedʵ�ַ�������**

��Ϊѧϰ֮�������ʵ�ַ����Ƚ�������⡣<br/>
�����������ַ�����Ҳͨ���������Ͻ�����һ�����˽⡣<br/>
��������ͨ��ģ��ʵ�����������������ģ�͵�ԭ��

```
import java.util.LinkedList;
import java.util.Queue;

public class ProducerAndConsumer {
    private final int MAX_LEN = 10;
    private Queue<Integer> queue = new LinkedList<Integer>();
    class Producer extends Thread {
        @Override
        public void run() {
            producer();
        }
        private void producer() {
            while(true) {
                synchronized (queue) {
                    while (queue.size() == MAX_LEN) {
                        queue.notify();
                        System.out.println("��ǰ������");
                        try {
                            queue.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                    queue.add(1);
                    queue.notify();
                    System.out.println("����������һ�����񣬵�ǰ���г���Ϊ" + queue.size());
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        }
    }
    class Consumer extends Thread {
        @Override
        public void run() {
            consumer();
        }
        private void consumer() {
            while (true) {
                synchronized (queue) {
                    while (queue.size() == 0) {
                        queue.notify();
                        System.out.println("��ǰ����Ϊ��");
                        try {
                            queue.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                    queue.poll();
                    queue.notify();
                    System.out.println("����������һ�����񣬵�ǰ���г���Ϊ" + queue.size());
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        }
    }
    public static void main(String[] args) {
        ProducerAndConsumer pc = new ProducerAndConsumer();
        Producer producer = pc.new Producer();
        Consumer consumer = pc.new Consumer();
        producer.start();
        consumer.start();
    }
}
```

## �ܽ�
������������ģʽ Ϊ��Ϣ���俪����һ��ո�µĸ����Ϊ�������ȼ���ߣ����Լ�ʹ���緢������ʱ��Ҳ������ͨ�������̶ȵı�֤���豸�İ�ȫ��<br/>
Ҳ��ȱ�㣬�����������еĸ����������Ƶġ�<br/>
������������ģʽ������ʱ�Ƚϼ򵥣�ʹ�÷��㰲ȫ���ڽ������Զ�����ҵ�ض�������������ͬ��<br/>
������������ģʽ����ʵֻҪ��֤�ڴ洢��ͬһʱ��ֻ��һ���̶߳���д�Ͳ��������⣬Ȼ����ȥ�����߳�ͬ����<br/>
����1��2��5���Ƚ����ƣ����Ǽ���������ͬһʱ��ֻ����һ������д��<br/>
������3��4��ʵ���ڴ洢�ڲ�ȥ��֤����д��Ψһ�ģ���Ͳ�϶�����ͨ����������ʵ�ֵģ�java�ײ���붼��װ���˶��ѡ�<br/>

���ڴ�ģ�͵���������ʵ�ַ��������Բο��������ݣ�<br/>
https://juejin.im/entry/596343686fb9a06bbd6f888c