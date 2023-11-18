---
title: python爬虫
date: 2023-09-04 15:18:39
tags: Python
description: The key record of python crawler.
---
#### 识别网页所用技术
构建网站所用的技术类型会对我们如何爬取信息产生影响。有一个十分有用的工具可以检查网站构建的技术类型--detectem 模块，该模块需要 python3.5+ 环境以及 Docker

#### python 读写文件
1. open() + close()
```
#先打开文件：
f = open('C:\\Users\\Administrator\\Desktop\\测试文件.txt','r',encoding = 'utf-8')

#再使用read()方法，查看文件里的内容：
print(f.read())

$关闭文件
f.close()
```
注意如果使用 `open`，结尾一定要使用close（）来关闭文件。原因主要是：
- 节约资源和内存耗损；
- 可以释放所占用的系统资源并尽早将文件置于更安全的状态，只有关闭文件后，文件内容才能同步到磁盘。
2. `with open` 推荐使用 
with 的作用相当于调用close（）方法，因此当我们使用with open( )在对文件操作完成后，无需通过close()关闭文件，文件会自动关闭，这种方法的安全系数更高，同时也避免了有些时候忘记关闭文件的毛病。
```
with open('file_name','r',encoding = 'utf-8') as f:
```
{%asset_img 读取操作类型.png%}
{%asset_img 读取操作类型.png%}

#### python requests 模块
python requests 是一个常用的 HTTP 请求库，可以方便地向网站发送 HTTP 请求，并获取响应结果。
```
response = requests.get(url=url, headers=headers)
```
返回一个 response 对象，该对象包含了具体的响应信息，如状态码、响应头(200 OK 404 NotFound)、响应内容等。
对于其中的content 和 text 属性

> content中间存的是字节码，而text中存的是Beautifulsoup根据猜测的编码方式将content内容编码成字符串。直接输出content，会发现前面存在b'这样的标志，这是字节字符串的标志，而text是，没有前面的b,对于纯ascii码，这两个可以说一模一样，对于其他的文字，需要正确编码才能正常显示。大部分情况建议使用.text，因为显示的是汉字，但有时会显示乱码，这时需要用.content.decode('utf-8')，中文常用utf-8和GBK，GB2312等。这样可以手工选择文字编码方式。

```
import requests

# 发送GET请求
url = 'https://example.com/some-page'
response = requests.get(url)

# 尝试获取内容的编码方式
encoding = response.apparent_encoding ## 来尝试获取爬取内容的编码方式。这个属性会尝试根据响应内容来猜测编码方式，通常用于解决服务器没有显式提供编码信息的情况。

# 设置编码方式并解码内容
content = response.content
text = content.decode(encoding)

# 打印内容
print(text)
```
通过这种方式，我们一般可以爬取网页的 `html` 代码。

#### python 标准库 os 模块
Python的os模块是一个用于与操作系统交互的内置模块。它提供了许多功能，允许你执行各种文件和目录操作，例如创建、删除、移动和重命名文件和目录，以及检查文件和目录的属性。下面是一些os模块的常见用法和功能：
1. 获取当前工作目录(current work directory)
```
current_directory = os.getcwd()
print(current_directory)
```
2. 列出目录中的文件和子目录
```
files_and_dirs = os.listdir('/path/to/directory')
print(files_and_dirs)
```
3. 创建目录
```
os.mkdir('/path/to/new_directory')
```
4. 删除目录
```
os.rmdir('/path/to/directory_to_delete')
```
5. 检查文件或者目录是否存在
```
if os.path.exists('/path/to/file_or_directory'):
    print("存在")
else:
    print("不存在")
```
其他 os 模块
{%asset_img os模块.png%} 

#### XPath
XPath（XML Path Language）是一种用于在XML文档中定位和选择元素的查询语言。它是一种重要的标准，广泛用于XML文档的解析和数据提取。XPath不仅可以用于XML文档，还可以用于HTML文档，因此它在Web开发和数据抓取中也非常有用。 (感觉可能类似于正则表达式？只是另一种不同的方式)
{%asset_img xpath.png%}
{%asset_img 未知节点.png%}

#### 正则表达式
`Regular Expression` 或者简称 `regex, RE`.
它的设计思想是用一种**描述性的语言**来给字符串定义一个规则，凡是符合规则的字符串，我们就认为它“匹配”了，否则，该字符串就是不合法的。

#### RE 库
RE 库就是正则表达式库，通过 RE 库我们可以匹配某些特定字符串的一些内容，比如爬虫爬取网页的时候，通过 RE 库可以获取网页内容中的某些特定标签内容。
量词：
{%asset_img 量词.png%}
字符类：
- `[]`: 匹配括号内的任意一个字符。例如 `[abc]` 匹配字符 a、b 或者 c
- `[^ ]`: 匹配括号内字符以外的任意一个字符。例如 [^abc] 就是除了 a、b或者c以外的任意字符。 
{%asset_img 转义字符.png%}

##### 常用函数
- `re.search(pattern, string, flags=0)` 在字符串中搜索第一个匹配的模式，并返回一个匹配对象。
- `re.match(pattern, string, flags=0)` 在字符串的开头匹配模式，并返回一个匹配对象。
- `re.findall(pattern, string, flags=0)` 返回一个包含所有匹配项的列表。
- `re.sub(pattern, repl, string, count=0, flags=0)` 用指定的替换字符串替换匹配的文本。
- `re.split(pattern, string, maxsplit=0, flags=0)` 根据模式拆分字符串。
其中 `flags` 是标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。
> 在Python中，前缀r表示一个原始字符串（raw string）。原始字符串中的反斜杠字符\会被当作普通字符处理，而不会被解释为转义字符。这在处理正则表达式等包含大量反斜杠的字符串时非常有用，因为正则表达式模式本身通常包含许多反斜杠，这些反斜杠需要被保留而不被解释为转义字符。

#### python 爬取图片简单示例
我们打开一个下载图片的网址 https://pic.netbian.com/new/
我们向这个网站发送请求以后获得的 `text` 就是网站的 `html` 代码。我们分析一下其中的 `html` 代码
{%asset_img html代码.png%}
其中的 `/uploads/allimg/xxx` 就是我们的图片的具体地址。
我们可以使用正则表达式(re 库)来获取 `html` 代码中所有符合图片格式的地址，然后存储到 `img` 中。再向图片的具体地址发送请求，此时我们使用 python 的文件读写(二进制模式)，就可以批量地将图片下载下来了。
```
import requests
import re
import os
from bs4 import BeautifulSoup
url = "https://pic.netbian.com/"
headers = {
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36 Edg/116.0.1938.69"
}
response = requests.get(url=url, headers=headers)
encoding = response.apparent_encoding
content = response.content
text = content.decode(encoding)
parr = re.compile('src="(/u.*?)".alt="(.*?)"') # 匹配图片链接和图片名字 使用正则表达式
image = re.findall(parr, text) # 所有的图片链接
path = "photos"
if not os.path.isdir(path):
    os.mkdir(path)
for i in image:
    link = i[0]
    name = i[1]
    with open(path+"/{name}.jpg".format(name),"wb") as img:
        res = requests.get("https://pic.netbian.com" + link)
        img.write(res.content)
        img.close()
    print(name+".jpg 获取成功......")
```
爬取王者荣耀头像，感觉写的很丑很傻。
```
import requests
import re
import os
url = "https://pvp.qq.com/web201605/herolist.shtml"
headers = {
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, "
                  "like Gecko) Chrome/116.0.0.0 Safari/537.36 Edg/116.0.1938.69"
}
response = requests.get(url=url, headers=headers)
encode = response.apparent_encoding
text = response.content.decode(encode)
pattern = re.compile(r'(//game.+\.jpg)')
pattern1 = re.compile(r'alt="(.+?)"')
images = re.findall(pattern, text)
names = re.findall(pattern1, text)
path = "heroes"
if not os.path.exists(path):
    os.mkdir(path)
cnt = 0
for element in images:
    cur = element
    with open(path + "/{}.jpg".format(names[cnt]), "wb") as img:
        res = requests.get("https:" + cur)
        img.write(res.content)
        img.close()
    print("捕获成功")
    cnt = cnt + 1
```

#### lxml 库
lxml 库是一个使用 python 编写的库，可以迅速、灵活地处理 XML 和 HTML。

其中 lxml.etree 模块是最常用的 HTML、XML 文档解析模块。其中lxml.etree.Element是处理xml的一个核心类，Element对象可以直观的理解为是XML中的节点。使用Element类，可以实现对XML节点、节点属性、节点内文本的操作。



https://blog.csdn.net/weixin_57440207/article/details/116363166 lxml 库的基本使用。

#### BeautifulSoup 示例
上面的都是比较基础的，对于一些动态的网页结构还是无能为力的。
我们可以使用 python `bs4` 库的 `BeautifulSoup` 库来对于请求后获得的 `html` 文本进行解析。
这是一段爬取豆瓣网站上`电影top250`的电影名称。
```
import requests
from bs4 import BeautifulSoup
headers = {
    "user-agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 '
                  '(KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36 Edg/116.0.1938.69'
}
for page_num in range(0, 250, 25):
    url = f"https://movie.douban.com/top250?start={page_num}&filter="
    response = requests.get(url=url, headers=headers)
    encode = response.apparent_encoding
    content = response.content.decode(encode)
    html = BeautifulSoup(content, 'lxml')
    titles = html.findAll("span", attrs={"class": "title"})
    for title in titles:
        if '/' not in title.string:
            print(title.string)
```
我们通过 `BeatifulSoup(content, 'lxml')` 获取的是一个 BeatifulSoup 解析得到的结构。
其中 content 就是我们请求网站获得的 html 代码，后面的 `lxml` 是一个 html 的解析器，我们需要手动指定解析器，因为 BeautifulSoup 不仅仅可以解析 html。
`html = BeautifulSoup(content, 'lxml')` 获得到的 html，有许多的方法。
其中如果我们想获得哪一元素，比如说段落，就可以直接 `html.findAll("p")` 返回的是一个可以迭代的对象。如果直接写 `html.find("p")` 则是获得的第一个段落元素。
如果我们仍想要对于段落进一步细化，我们可以在后面加上参数，其中的格式是若干组键值。比如，我们想获取类名为`title`的span，就可以写为 `titles = html.findAll("span", attrs={"class": "title"})`
对于提取到的元素，我们会获得一个 `bs4.element.Tag` 就是一个 bs4 中的 Tag 对象，比如说我们有一个 `cur` 是 `bs4.elemnt.tag` 对象。
`cur.name` 就是输出标签的名字，比如 `p` `img` `div`
如果我们想要获得里面的单个属性值，就直接 `cur['xx']` 或者 `cur.get('xx')`，如果我们想获取全部的属性值，就是 `cur.attrs`
获得标签内的文本，`cur.get_text()`

#### Selenium
前面都是模拟发送一个 `request` 获得返回，下面是真是模拟我们打开浏览器后进行操作。
Python 中的 Selenium 是一个用于自动化网页操作和测试的强大工具。它提供了一种方式来模拟用户在浏览器中的操作，例如打开网页、填写表单、点击按钮、抓取数据等。
Selenium 的核心之一就是 WebDriver，它是一个接口，允许我们与不同的浏览器进行交互。我们需要下载与我们所使用浏览器相对应的 WebDriver 驱动程序。将 WebDriver 的路径指定为您的 Python 脚本中。

下面是一段打开百度首页并且搜索「你好」的代码。
```
from selenium import webdriver
import time
from selenium.webdriver.common.by import By # 使用 find_element by=xxx 一定要引入这个
driver = webdriver.Chrome()
driver.get('https://www.baidu.com')
driver.find_element(by=By.ID, value='kw').send_keys('你好')
driver.find_element(by=By.ID, value='su').click()
time.sleep(5)
```
下面是查找元素的 by 赋值情况，后面的 `value` 就是目标的索引值。这是新版本的 `find` 操作，之前的 `find_element_by` 方法现在已经弃用。
{%asset_img selenium定位元素.png%}

对于查找后，如果是 `find_elements` 得到的是一个链表，如果是 `find_element` 得到的是一个 `<class 'selenium.webdriver.remote.webelement.WebElement'>`，后面对于这个类元素，我们可以 `xxx.click()` 点击
`xxx.send_keys("xxx")` 发送信息
`xxx.text` 获取文本 
`xxx.clear()` 清除元素内容 如 input 中的内容
`get_attribute("value")` 获得`value`的属性值 
`current_url` 可以获取当前页面的 url

下面是更深入的对于鼠标和键盘
模拟鼠标操作需要读入类 `ActionChains`
`from selenium.webdriver.common.action_chains import ActionChains`
{%asset_img 鼠标操作.png%}

模拟键盘操作的话，也需要导入键盘的类
`from selenium.webdriver.common.keys import Keys`
{%asset_img 键盘操作.png%}

##### 延时等待
遇到使用ajax加载的网页，页面元素可能不是同时加载出来的，这个时候尝试在get方法执行完成时获取网页源代码可能并非浏览器完全加载完成的页面。所以，这种情况下需要设置延时等待一定时间，确保全部节点都加载出来。
有三种方式：
1. 强制等待
直接 `time.sleep(xx)`(记得先导入包 `import time`)
2. 隐式等待
`implicitly_wait(xx)` 设置等待时间，如果到时间还有元素没有加载出来就会抛出异常。
3. 显式等待
设置一个等待时间和等待条件，在规定时间内，每隔一段时间查看下条件是否成立，如果成立那么程序就继续执行，否则就抛出一个超时异常。

##### 对 Cookie 的操作(亦称为 Http Cookie)
Cookie 通常用于在客户端（浏览器）和服务器之间存储一些小型数据，以便在用户与网站进行交互时进行识别、跟踪和状态管理。
{%asset_img 存储信息.png%}
爬虫中常常使用 selenium + requests 实现 cookie持久化，即先用 selenium 模拟登陆获取 cookie ，再通过 requests 携带 cookie 进行请求。
`webdriver` 提供 cookie 的几种操作：读取、添加和删除。
1. get_cookies：以字典的形式返回当前会话中可见的 cookie 信息。
2. get_cookie(name)：返回 cookie 字典中key == name 的 cookie 信息
3. dd_cookie(cookie_dict)：将 cookie 添加到当前会话中
4. delete_cookie(name)：删除指定名称的单个 cookie
5. delete_all_cookies()：删除会话范围内的所有cookie

https://blog.csdn.net/kobepaul123/article/details/128796839
https://blog.csdn.net/weixin_50835854/article/details/117170894 selenium 爬取图片
https://zhuanlan.zhihu.com/p/270391233
https://blog.csdn.net/qq_37267676/article/details/111667266
https://zhuanlan.zhihu.com/p/366773104

```
from selenium import webdriver
from selenium.webdriver.common.by import By
import time
driver = webdriver.Chrome()
for index in range(0, 250, 25):
    driver.get(f'https://movie.douban.com/top250?start={index}&filter=')
    time.sleep(1)
    list = driver.find_elements(by=By.XPATH, value='//div[@class="pic"]/a/img')
    for cur in list:
        print(cur.get_attribute('alt'))

```
#### selenium 和 splinter
splinter和selenium都是用于测试网页的程序，可以模拟浏览器操作，进行自动化测试，可以用于爬虫，自动抢票，网页自动化处理等。Selenium是Splinter的底层，Splinter是Selenium的一个上层封装。使用splinter和selenium时也会用到和html，css相关的使用。

#### Scrapy 框架
`Scrapy` 是一个异步网络 python 爬虫框架，可以高效地处理大量的请求和响应。它能够并行发送HTTP请求，从而加快数据抓取速度。异步处理允许我们同时处理多个请求而无需等待每一个请求的完成，这对于大规模的数据抓取任务十分有用。
它的优势：
1. 内置选择器(Selector)，使用 XPath 或者 CSS 选择器语法，使我们可以轻松获取 HTML 文档中的数据(我们不需要再去使用 bs4 ?)。
2. 模块化和可扩展性
允许我们将爬虫任务分解为多个模块，包括爬虫、中间件、管道等，使代码易于维护和扩展。
3. 自动化处理
Scrapy提供了强大的自动化功能，包括请求的调度、URL跟踪、重试失败的请求等。它还支持自动限速，以避免过度请求目标网站，从而遵守网站的使用政策。
4. 内置 HTTP 请求处理
Scrapy可以处理HTTP请求和响应的所有细节，包括Cookies、User-Agent、重定向、状态码处理等。这减轻了用户的负担，让你专注于爬取和数据处理。

https://www.runoob.com/w3cnote/scrapy-detail.html 上面讲解了 Scrapy 的爬行流程，感觉还是挺形象的。只有当调度器中不存在任何 request 的时候，整个程序才会停止，又因为对于下载失败的 url 会再次进入 scheduler(调度器)，所以对于下载失败的 url，Scrapy 会重新进行下载。


