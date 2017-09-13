### find\_all\( name , attrs , recursive , text , \*\*kwargs \) {#articleHeader10}

### find\( name , attrs , recursive , text , \*\*kwargs \) {#articleHeader11}

它与`find_all()`方法唯一的区别是`find_all()`方法的返回结果是值包含一个元素的列表,而`find()`方法直接返回结果,就是直接返回第一匹配到的元素，不是列表，不用遍历，如`soup.find("p").get("class")`

### 通过标签名查找 {#articleHeader13}

```py
print soup.select('title') 
#[<title>The Dormouse's story</title>]


print soup.select('a')
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>, <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>, <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

### 通过类名查找 {#articleHeader14}

```
print soup.select('.sister')
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>, <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>, <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]
```

### 通过id名查找 {#articleHeader15}

```
print soup.select('#link1')
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>]
```

### 组合查找 {#articleHeader16}

学过 css 的都知道 css 选择器，如 p \#link1 是查找 p 标签下的 id 属性为 link1 的标签

```py
print soup.select('p #link1')    #查找p标签中内容为id属性为link1的标签
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>]

print soup.select("head > title")   #直接查找子标签
#[<title>The Dormouse's story</title>]
```

### 属性查找 {#articleHeader17}

查找时还可以加入属性元素，属性需要用中括号括起来，注意属性和标签属于同一节点，所以中间不能加空格，否则会无法匹配到。

```py
print soup.select('a[class="sister"]')
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>, <a class="sister" href="http://example.com/lacie" id="link2">Lacie</a>, <a class="sister" href="http://example.com/tillie" id="link3">Tillie</a>]


print soup.select('a[href="http://example.com/elsie"]')
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>]
```

同样，属性仍然可以与上述查找方式组合，不在同一节点的空格隔开，同一节点的不加空格,代码如下：

```py
print soup.select('p a[href="http://example.com/elsie"]')
#[<a class="sister" href="http://example.com/elsie" id="link1"><!-- Elsie --></a>]
```

以上的 select 方法返回的结果都是列表形式，可以遍历形式输出，然后用 get\_text\(\) 方法来获取它的内容

```py
soup = BeautifulSoup(html, 'lxml')
print type(soup.select('title'))
print soup.select('title')[0].get_text()

for title in soup.select('title'):
    print title.get_text()
```



