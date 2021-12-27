请求：

```
请求行 -> 	请求方式(get/post) 请求URL地址 协议
请求头 -> 	放一些服务器要使用的附加信息（重点）
(request header)比如人机识别、爬与反爬机制等
请求体 ->	请求参数（具体要请求获取的信息）
```

请求头中比较重要的是：

	1. User-Agent：请求载体的身份标识（包含了你使用哪个浏览器、什么设备等信息）
	2. Reference：防盗链（这次请求从哪个页面来的？反爬会用到）
	3. cookie：本地字符串数据信息（用户登录信息，反爬的token）

响应：

```
状态行 ->	协议 状态码(status code)
响应头 ->	放一些客户端要使用的附加信息（重要）
(response header)cookies，密钥等
响应体 ->	服务器返回的真正客户端要用的内容（HTML,JSON）等
```

响应头中比较重要的是：

 	1. cookie：本地字符串数据信息（用户登录信息，反爬的token）
 	2. 其他token字样

状态码：

	1. 200 正常
	2. 404 请求的地方不存在/页面丢失
	3. 500 服务器报错
	4. 302 重定向

​	

下面正式开始代码的学习：

#### 基础爬虫

##### 百度浏览器信息搜索（get请求）

```python
import requests
query = input("please input what you want to search for: ")
print(type(query))
url = f'https://www.baidu.com/s?wd={query}'
# 伪装成用浏览器访问
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.81 Safari/537.36 SE 2.X MetaSr 1.0"}
# 发出get请求，获得响应
resp = requests.get(url=url, headers=headers)
# 获得页面源代码
print(resp.text)
# 访问完一定要记得删掉鸭
resp.close()
```

##### 模拟百度翻译（post请求）

data从From_data中获取

```python
url ='https://fanyi.baidu.com/sug'
word = input('please input what you want to translate:')
data = {"kw": word}
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36 Edg/95.0.1020.30"}
# post请求发送的数据必须放在字典中，通过data参数进行传递
resp = requests.post(url=url, data=data, headers=headers)
# 将服务器返回的内容全部处理成json() => dict
print(resp.json())
resp.close()
```

##### 爬取豆瓣电影中排名前100的动画电影并且以比较易读的方式输出

get请求中 ”?“ 后面是参数，亦可从Query String Parameters中获取易读版

==XHR一般为重定向数据==

```python
import requests
import json
url = 'https://movie.douban.com/j/chart/top_list'
params = {
    'type': '25',
    'interval_id': '100:90',
    'action':'',
    'start': '0',
    'limit': '100',
}
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36 Edg/95.0.1020.30"}
resp = requests.get(url=url, params=params, headers=headers)
output = resp.json()
# json.dumps序列化时对中文默认使用的ascii编码，要取消默认操作
print(json.dumps(output, indent=True, ensure_ascii=False))
resp.close()
```



##### 将网页的html源代码全部写入本地html文件中

```python
url = 'https://umei.cc/bizhitupian/weimeibizhi/'
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36 Edg/95.0.1020.30"}
resp = requests.get(url=url, headers=headers)
# 防止输出的中文乱码
resp.encoding = 'utf-8'
file = open('bizhi.html', 'w', encoding='utf-8')
file.write(resp.text)
file.close()
```

##### 读取本地html文件

```python
file = open('bizhi.html', 'r', encoding='utf-8')
text = file.read()
```



#### 数据清洗

1.

Regular Expression（正则表达式）：一种使用表达式的方式对字符串进行匹配的语法规则

正则的语法：使用<u>元字符</u>进行排列组合用来匹配字符串

元字符：具有固定含义的特殊字符

##### 常用元字符：

代码	              说明
.				匹配除换行符以外的任意字符
<u>\w			匹配字母或数字或下划线</u>
\s			匹配任意的空白符
<u>\d			匹配数字</u>
\b			匹配单词的开始或结束
^			匹配字符串的开始（用于校验数据合法性）
$			匹配字符串的结束（用于校验数据合法性）

--------------------------

***常用的反义代码（大写）***

\W			匹配任意不是字母，数字，下划线，汉字的字符
\S			匹配任意不是空白符的字符
\D			匹配任意非数字的字符
\B			匹配不是单词开头或结束的位置
[...]		  匹配字符组中的任意字符（其中的-表示范围，如a-z表示26个小写字母）
\[^...\]		匹配除了aeiou这几个字母以外的任意字符



##### 量词：控制前面的元字符出现的次数

\* 				重复零次或更多次

\+				重复一次或更多次
?	        	重复零次或一次
{n}	        重复n次
{n,}	        重复n次或更多次
{n,m}	     重复n到m次

##### ==贪婪匹配和惰性匹配==

.*			 贪婪匹配，匹配尽可能长的

<u>.*?			惰性匹配（当出现多个匹配，选最短的）</u>



##### re库

`re.findall(pattern, string, flag)`

pattern：元字符

flag:特殊规则，如flag=re.S: 让 "." 也能匹配换行符

以列表的形式返回

`re.finditer(pattern, string)`

以迭代器的形式返回，拿数据需要.group()

`re.search(pattern, string)`

在全文中找到一个结果就返回，返回match对象，拿数据需要.group()

`re.match(pattern, string)`

从头开始匹配



`re.compile(pattern)`

预加载一个正则表达式，之后可以一直用

举个例子：

```python
import re
obj = re.compile(r"\d+")
ret = obj.finditer("我叫2333，我npy叫2201")
for i in ret:
    print(i.group())
ret2 = obj.findall("我是2001年2月出生的")
print(ret2)

输出结果：
2333
2201

['2001','2']


```

##### 从HTML代码中提取想要的信息

```python
import re
s = "<div class='hebe'><span id='1'>终身大事</span></div>"
# (?P<name>正则表达式) 可以单独从正则匹配内容中提取出名字为name的内容
# flag=re.S: 让 "." 也能匹配换行符
obj = re.compile(r"<div class='.*?'><span id='\d+'>(?P<song>.*?)</span></div>", re.S)
result = obj.finditer(string=s)
for i in result:
    print(i.group("song"))
```



strip()

 用于移除字符串头尾指定的字符（==默认==为空格或换行符）或字符序列。

```python
s = '   abc'
s = s.strip()
print(s)

输出结果：'abc'
```



##### bs4库

HTML经典语法：

```html
<标签 属性=“值” ... 属性=“值”>
    被标记的内容
</标签>
```

通过HTML中的标签名称来拿到数据

```python
import requests
from bs4 import BeautifulSoup
...
# 1.把页面源代码交给BeautifulSoup进行处理，生成bs对象
# 需指明你传入的文件的类型，如html,xml等
page = BeautifulSoup(resp.text, "html.parser")
# 2.从bs对象中查找数据
# 用于截取这个标签+属性值...中被标记的内容
# find(标签， 属性=值)
# find_all(标签， 属性=值)
page.find("table", class_="value") #由于class是python关键字，故加一个_避免报错
```

##### 举个例子，获取唯美壁纸这个网站中的所有图片链接

```python
from bs4 import BeautifulSoup
url = 'https://umei.cc/bizhitupian/weimeibizhi/'
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36 Edg/95.0.1020.30"}
resp = requests.get(url=url, headers=headers)
# 防止输出的中文乱码
resp.encoding = 'utf-8'
text = resp.text
page = BeautifulSoup(text, 'html.parser')
alist = page.find("div", class_="TypeList").find_all("a")
# 再拿到每一项其中的属性href的值（发现不完整，需人为做个拼接）
for i in alist:
    i = 'https://umei.cc' + i.get('href')
    print(i)
```

*如果要获取标签内部的东西，用bs4比用re更方便！！！*



欲爬取“中国新闻网”中的新冠信息，接收到的响应为：`<Response [521]>`

经网上查询可知，该网站有反爬机制，需要在headers中增加一项cookies来反反爬

cookies从Request Headers的Cookies项中获取

