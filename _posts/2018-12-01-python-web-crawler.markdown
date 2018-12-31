---
layout: post
title: " Web Crawler "
subtitle: "Python learning -- Web Crawler example"
author: "Bing Yan"
header-img: "img/web-crawler/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Python
  - Learning
---
## ǰ��

&ensp;&ensp;&ensp;&ensp;Python ��һ���߲�εĽ���˽����ԡ������ԡ������Ժ��������Ľű����ԡ�<br/>
Python ����Ҳ��������������Է�չ������,����� ABC��Modula-3��C��C++��Algol-68��SmallTalk��Unix shell �������Ľű����Եȵȡ�<br/>
�� Perl ����һ����Python Դ����ͬ����ѭ GPL(GNU General Public License)Э�顣<br/>
&ensp;&ensp;&ensp;&ensp;Python ����ƾ��к�ǿ�Ŀɶ��ԣ�����������Ծ���ʹ��Ӣ�Ĺؼ��֣��������Ե�һЩ�����ţ������б��������Ը�����ɫ�﷨�ṹ��<br/>
&ensp;&ensp;&ensp;&ensp;����������ʼ�Ӵ�Python����ͨ���������档�����Ҿ�ͨ��һ���Լ���д���������������������˽�һ��Python��

## ����
### ʲô����������(Web Crawler)

&ensp;&ensp;&ensp;&ensp;����˵����������һ����վ��������豸��ɵĴ���������ͨ�����������վ�㣬վ���HTML��JS��CSS���뷵�ظ����������Щ���뾭���������������Ⱦ�����ḻ��ʵ���ҳ����������ǰ��<br/>
&ensp;&ensp;&ensp;&ensp;������ǰѻ���������һ�Ŵ��֩���������ݱ��Ǵ����֩�����ĸ����ڵ㣬���������һֻС֩�룬��������ץȡ�Լ���������ݣ�����ָ���ǣ�����վ�������󣬻�ȡ��Դ���������ȡ�������ݵĳ���<br/>
&ensp;&ensp;&ensp;&ensp;�Ӽ���������˵���� ͨ������ģ�����������վ�����Ϊ����վ�㷵�ص�HTML����/JSON����/���������ݣ�ͼƬ����Ƶ�� �������أ�������ȡ�Լ���Ҫ�����ݣ��������ʹ�á�

### ��������(Web Crawler)����ʲô
<br/>

*   ��Ϊͨ������������ҳ�ռ���(google,baidu)
*   ����ֱ��������
*   ��ѧ�о�������������Ϊ��������Ⱥ�ݻ������ද��ѧ�о����������ѧ���������磬�����ھ򣬵������ʵ֤�о�����Ҫ�������ݣ������������ռ�������ݵ�������
*   ͵����hacking���������ʼ�����
<br/>
�ҵ���⣺���Ǵ������л�ȡ��Ҫ�Ĵ������ݣ���Ϊ�����ݵȼ���������ԭ�ϡ���Ϊ���������ݱ������̺��źܶ���ɣ���Ҫȥ���ֺ��ھ�ġ����ⲿ�ֹ�������Ҫ֮���������ϴ�����ݲִ������ݷ����ȼ����ֶΡ�
<br/>


### Ϊʲô��Pythonд��������

�������Զ�����ͨ���ô�������д��������Ҳ�кܶ�������ѡ��<br/>
��������ģʽ����Ҫ�أ�<br/>

*   C��C++����Ч�ʣ����٣��ʺ�ͨ������������ȫ����ȡ��ȱ�㣬��������д�����ֳ��ֳ������磺��������Դ���롣
*   �ű����ԣ�Perl, Python, Java, Ruby���򵥣���ѧ�����õ��ı������ܷ�����ҳ���ݵ�ϸ����ȡ����Ч���������ߣ��ʺ϶�������վ�ľ۽���ȡ
*   C#��ò����Ϣ������˱Ƚ�ϲ�������ԣ�
<br/>

������Ϊʲôpython�ܹ�ʤ�����������Ϊ������˽��ܣ�<br/>

*   ��ƽ̨����Linux��windows���в����֧�֡�
*   ��ѧ���㣬��ֵ��ϣ�Numpy��Scipy
*   ���ӻ���2d��Matplotlib(��ͼ��Ư��), 3d: Mayavi2  
*   �������磺Networkx
*   ͳ�ƣ���R���Խӿڣ�Rpy
*   ����ʽ�ն�
*   ��վ�Ŀ��ٿ���

<br/>

### ����Ļ�������
<br/>
�û���ȡ�������ݵķ�ʽ��<br/>

*   ������ύ����--->������ҳ����--->������ҳ��<br/>
*   ģ���������������(��ȡ��ҳ����)->��ȡ���õ�����->��������ݿ���ļ���<br/>
����Ҫ���ľ��Ƿ�ʽ2��

![](/img/web-crawler/wc-1.png)
<br/>
 1. ��������:<br/>
>ʹ��http����Ŀ��վ�㷢�����󣬼�����һ��Request<br/>
Request����������ͷ��������� <br/>
Requestģ��ȱ�ݣ�����ִ��JS ��CSS ����<br/>

 2. ��ȡ��Ӧ����:<br/>
>�����������������Ӧ�����õ�һ��Response<br/>
Response������html��json��ͼƬ����Ƶ��<br/>

 3. ��������:<br/>
> ����html���ݣ�������ʽ��REģ�飩����������������Beautifulsoup��pyquery�ȡ�
����json���ݣ�jsonģ�� <br/>
��������������:��wb�ķ�ʽд���ļ�<br/>

 4. ��������:<br/>
>���ݿ⣨MySQL��Mongdb��Redis��<br/>
�ļ�<br/>


### HTTPЭ�鸴ϰ
��д����������Ҫ��HTTPЭ����һ���˽⡣ͨ���޸�����ʽ������URL������Ӧ���й���������Ϣ����ʵ����������Ĺ��ܡ�
<br/>
![](/img/web-crawler/wc-2.png)
<br/>
��ͼ��֪���û�ͨ�������������������������������������Ӧ��������������Request��Response������Ϣ��<br/>
*   Request���û����Լ�����Ϣͨ���������socket client�����͸���������socket server��<br/>
*   Response���������������󣬷����û�������������Ϣ��Ȼ�󷵻����ݣ����ص������п��ܰ����������ӣ��磺ͼƬ��js��css�ȣ�<br/>

**Request���:**

*   ����ʽ:����������ʽ��GET / POST
*   �����URL:URL��ȫ��ͳһ��Դ��λ�����������廥������һ��Ψһ����Դ ���磺һ��ͼƬ��һ���ļ���һ����Ƶ��������urlΨһȷ��
*   ����ͷ:
    * User-agent:����ͷ�����û��user-agent�ͻ������ã�����˿��ܽ��㵱��һ���Ƿ��û�host
    * cookies:cookie���������¼��Ϣ
    * Referrer:����Դ����������һЩ������վ����ͨ��Referrer �����������ԣ���������ҲҪע��ģ�⣩
*   ������:�����get��ʽ��������û������ ��get�������������� url��������У�ֱ���ܿ����������post��ʽ����������format data

**Response���:**

*   ��Ӧ״̬��:
    * 200������ɹ�
    * 301��������ת
    * 404���ļ�������
    * 403����Ȩ�޷���
    * 502������������
    
*   ��Ӧͷ:
    * Set-Cookie:BDSVRTM=0; path=/�������ж���������������������cookie��������
    * Content-Location���������Ӧͷ�а���Location���������֮��������ͻ����·�����һ��ҳ��

*   preview:������ҳԴ����,����JSO���ݡ���ҳhtml��ͼƬ�����������ݵȡ�

### Sina News Web Crawler

������ѵ��Ƶ��һ��һ������˵�һ����������--���������������棺<br/>
�������̲�����˳����������������Ҫ�У�<br/>
*   ��վ��ַ�������Ƶ������Ҫ����ά������Ҳ�Ǹ�����վ�������һ���ֶΡ���Ϊ��д�����������ľ���URL��ʽ��ͳһ������ȫ�Զ���Ҫ��ɡ�ȫ���Լ������ˡ�
*   �ܶ���ҳ�ϵ���Ϣ��ͨ�����������ؽ����ģ�Ҫ֪��һ����ҳ��չʾ��������Ҫ�������ϰٸ������������ЩResponse���ҵ���ȷ����ϢҲ��Ҫϸ�ġ�����������еġ��������������Ҽ�ʹ����������Ӻ��޸ģ������������ռ�Ҳ���ǻ��в�������

����Ŀ������[Github](https://github.com/Icyfighting/Web-Crawler-of-Sina-News-Website)

```
commentCountUrl = 'https://comment5.news.sina.com.cn/cmnt/count?format=json&newslist=gn:comos-{}:0'
commentCountUrl2 = 'https://comment.sina.com.cn/page/info?version=1&format=json&channel=cj&newsid=comos-{}'
import re
import requests
from bs4 import BeautifulSoup
import json
from datetime import datetime
def getCommentCount(newsurl):
    m = re.search('doc-i(.+).shtml',newsurl)  #��������url�ҳ����ŵ�id
    newsid= m.group(1)
   # print(newsid)
    commentCountUrlFormat = commentCountUrl.format(newsid)   #��������id����ϳ���������������
    commentCountUrlFormat2 = commentCountUrl2.format(newsid)
    #���������������ӣ�ȡ��������
    res = requests.get(commentCountUrlFormat)
    res2 = requests.get(commentCountUrlFormat2)
    res.encoding='utf-8'
   # print(res.text)
    mm = re.search('\"total\":.*?(?=,)',res.text)
    mm2 = re.search('\"total\":.*?(?=,)',res2.text) #������·����ֻ��һ�����з���ֵ�ģ���һ��û�з���ֵ����Ҫ�ж�
    commentCount1=0
    commentCount2=0
    if mm is not None:
        commentCountStr1 = mm.group(0).lstrip('"total":').strip()
        commentCount1 = int(commentCountStr1)
    if mm2 is not None:
        commentCountStr2 = mm2.group(0).lstrip('"total":').strip()
        commentCount2 = int(commentCountStr2)
    
    #���ڶ�����ַ������ȷ �����ǵ�һ����ַ����Ҳ���ǿգ�֪ʶ������0�����Բ�Ϊ�յĶ�Ҫȡ��Ȼ�󷵻ش��������
    
    
    if commentCount1 > commentCount2:
        return commentCount1
    else:
        return commentCount2
  
```
```
def getAuthor(soup):
    
    show_author = soup.select('.show_author')
    article_editor = soup.select('.article-editor')
    if len(show_author)>0:
        return show_author[0].text.lstrip('���α༭��') 
    elif len(article_editor)>0:
        return article_editor[0].text.lstrip('���α༭��')
    else:
        return 'null'
```
```
def getNewsDetail(newsurl):
    result = {}
    res = requests.get(newsurl)
    res.encoding='utf-8'
    soup = BeautifulSoup(res.text,'html.parser')
    result['title'] = soup.select('.main-title')[0].text
    result['dt'] = datetime.strptime(soup.select('.date')[0].text,'%Y��%m��%d�� %H:%M')
    result['newssource'] = soup.select('.source')[0].text
    result['article'] = ' '.join([p.text.strip() for p in soup.select('.article p')[:-1]])
    result['editor'] = getAuthor(soup)
    result['commentsCount'] = getCommentCount(newsurl)
    return result
```
```
def parseListLinks(pageUrl):
    newsdetails = []
    res = requests.get(pageUrl)
    res.encoding='utf-8'
    jd = json.loads(res.text)
    for ent in jd['result']['data']:
        newsdetails.append(getNewsDetail(ent['url']))
    return newsdetails
```
```
def getNewsTotal(start, end):
    pageCommonUrl = 'https://feed.mix.sina.com.cn/api/roll/get?pageid=153&lid=2509&k=&num=10&page={}'
    if str(start).isdigit() and str(end).isdigit():
        if int(start)< int(end):
            news_total = []
            for i in range(int(start),int(end)):
                newsurl = pageCommonUrl.format(i)
                newsary = parseListLinks(newsurl)
                news_total.extend(newsary)
            return news_total
        else:
            return None
    else:
        return None
```
```
import pandas
df = pandas.DataFrame(getNewsTotal(11,13))
df.head(20)
```
<br/>
ִ��Ч����ͼ��<br/>

![](/img/web-crawler/wc-3.png)

<br/>

��ȻҲ����ͨ���������洢�����ݿ���߱���С�
```
df.to_excel('news_result.xlsx')
```


## �ܽ�
&ensp;&ensp;&ensp;&ensp;���˶�Python����⻹�����ǽű����ԡ���ʵPython��һ��ȫ��ѡ�֣��������ڿ���������Ǵ����ʡ�
��֪���Ͽ�������[���㶼�� Python ����ʲô����](https://www.zhihu.com/question/20799742)����Ļظ�������˵��ֻ���벻��û���������ġ�


## �ο�����
�˴�ѧϰ��Ҫ���������漼����վ:<br/> 
https://study.163.com/course/courseMain.htm?courseId=1003285002 <br/>
