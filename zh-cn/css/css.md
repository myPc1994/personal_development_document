# css的知识点

#### 1、CSS控制文字，超出部分显示省略号

![](../../images/css/omit.png '相当于img的title')
```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```

![](../../images/css/omit2.png '相当于img的title')
```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```


#### 2、文字画线
##### 标签形式
![](../../images/css/delLine.jpg '相当于img的title')
```html
<del>del标签删除线</del><br/>
<strike>strike标签删除线</strike><br/>
<s>s标签删除线</s> <br/>
<u>u标签下划线</u><br/>
<p style="text-decoration: underline;">样式设置下行线</p></FONT><br/>
<b>加粗文字</b> <br/>
<i>斜文字</i> <br/><br/>
<tt>等宽字体</tt> <br/>
上标<sup>2</sup> <br/>
下标<sub>20</sub> <br/>
```

##### css样式
<p style="text-decoration:line-through;">删除线</p>
<p style="text-decoration:underline;">下划线</p>
<p style="text-decoration:overline;">顶划线</p>
<p style="text-decoration:underline overline line-through;">三种同时</p>
<p style="text-decoration:blink;">闪烁</p>

```css
    text-decoration:line-through;  删除线
    text-decoration:underline;     下划线
    text-decoration:overline;    顶划线
    text-decoration:underline overline line-through; 三种同时
    text-decoration:blink;   闪烁
```