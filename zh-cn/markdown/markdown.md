## Markdown语法

### 1、标题

```markdown
# h1
## h2
### h3
#### h4
##### h5
###### h6

```
### 2、引用
###### 单行式
> hello world!

```markdown
    > hello world!
```

###### 多行式

> hello world!
hello world!
hello world!

```markdown
    > hello world!
    hello world!
    hello world!
```


###### 多层嵌套
> aaaaaaaaa
>> bbbbbbbbb
>>> cccccccccc

```markdown
    > aaaaaaaaa
    >> bbbbbbbbb
    >>> cccccccccc
```


### 3、行内标记
标记之外`hello world`标记之外
```markdown
    标记之外`hello world`标记之外
```
### 4、代码块
##### 使用 “```”包围着
```markdown
<div>
    <div></div>
    <div></div>
    <div></div>
</div>
```
    ```语言
    代码内容
    ```

##### Tab 使用tab缩进

### 5、插入链接
##### 内链式
[百度1](http://www.baidu.com)
```markdown
[百度1](http://www.baidu.com)
```
##### 引用式
[百度2][2]
[2]: http://www.baidu.com/
```markdown
[百度2][2]
[2]: http://www.baidu.com/
```

### 6、插入图片
##### 内链式
![](./images/logo.png '相当于img的title')
```markdown
![](./images/logo.png '相当于img的title')
```
##### 内链式带连接
[![](./images/logo.png '百度')](http://www.baidu.com)
```markdown
[![](./images/logo.png '百度')](http://www.baidu.com)
```

### 7、序表
##### 有序
注：序列.后 保持空格
1. one
2. two
3. three

```markdown
1. one
2. two
3. three
```
##### 无序
* one
* two
* three

```markdown
* one
* two
* three
```
##### 序表嵌套
1. one
    1. one-1
    2. two-2
2. two
    * two-1
    * two-2

```markdown
1. one
    1. one-1
    2. two-2
2. two
    * two-1
    * two-2
```
##### 序表嵌套代码块
注：换行+两个Tab
* one

    var a = 10;     // 与上行保持空行并 递进缩进

```markdown
* one

    var a = 10;     // 与上行保持空行并 递进缩进
```
### 8、任务列表
这是文字……
- [x] 选项一
- [ ] 选项二
- [ ]  [选项3]

```markdown
这是文字……
- [x] 选项一
- [ ] 选项二
- [ ]  [选项3]
```


### 9、表格
注： : 代表对齐方式 ,** : 与 | 之间不要有空格**，否则对齐会有些不兼容

|    a    |       b       |      c     |
|:-------:|:------------- | ----------:|
|   居中  |     左对齐    |   右对齐   |
|=========|===============|============|

```markdown
|    a    |       b       |      c     |
|:-------:|:------------- | ----------:|
|   居中  |     左对齐    |   右对齐   |
|=========|===============|============|

```
> 简约写法

a  | b | c
:-:|:- |-:
    居中    |     左对齐      |   右对齐
============|=================|=============

```markdown
a  | b | c
:-:|:- |-:
    居中    |     左对齐      |   右对齐
============|=================|=============
```

### 10、分隔符
---
```markdown
    ---
```

### 11、符号转义
\_不想这里的文本变斜体\_

\#\*不想这里的文本被加粗\*\*
```markdown
    \_不想这里的文本变斜体\_

    \#\*不想这里的文本被加粗\*\*
```

