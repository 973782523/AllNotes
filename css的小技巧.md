### 垂直居中

1. 单行文字

```css
height:20px;
line-height:20px;
```

2. 多行文字

```css
外部<div>
div{
    display:table-cell;//子div在父div实现了垂直居中
    vertaical-align:middle;//两个配合使用
}
内部<span>
span{
    display:inline-block;
}
```

3. 图片

```css
<img>外部<div>
div{
    display:table-cell;
    text-align:center;
    vertical-align:middle;
}
如果外层是<a>标签
a{
    display:inline-block;
    text-align:center;
    vertical-align:middle;   
}
img{
    vertical-align:middle;
}
```

###鑫三无准则 

> 无浮动，无宽度，无图片 

### calc

