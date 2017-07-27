# Less
Less学习笔记与一个简单项目
# say hello & intro
- Less is More,Than CSS-少即是多，比CSS
## less介绍-say hello

 
### Less是什么？
 **Less 类似于Jquery**
 
-  LESSCSS是一种动态样式语言，属于CSS预处理语言的一种，它使用类似CSS的语法，为CSS的赋予了动态语言的特性，如变量、继承、运算、函数等，更方便CSS的编写和维护。
- LESSCSS可以在多种语言、环境中使用，包括浏览器端、桌面客户端、服务端。



# Koala的基本使用
## koala编译
  - Koala
  - 国人开发的LESS/SASS编译工具。
  - 下载地址：[**http://koala-app.com/index-zh.html**](http://koala-app.com/index-zh.html)

## Node.js库编译 
  - npm install -g less
  - lessc test.less > test.css（注意less文件与css文件路径）
## 浏览器端编译

# Less语法详解
## Less注释

less代码

```
/*我是被编译的*/

//不会被编译
```

css代码


```
/*我是被编译的*/
```


  
  

## 变量
  - less中想要声明变量的话 一定要用@开头 例如： @变量名：值；

less代码


```
//变量

@test_width:300px;

.body{
  width:@test_width;
  height:@test_width;
  background-color: yellow;

  .border;

  left:100px;
}
```


 css代码


```
.body {
  width: 300px;
  height: 300px;
  background-color: yellow;
  border: 5px solid pink;
  left: 100px;
}
```


## 混合

### 混合(mixin)变量
例如：
```
.border{border:solid 10px red;}
```

### 带参数的混合

```
.border-radius (@radius) {css代码}
```


可设定默认值


```
border-radius(@radius:5px){css代码}
```

### 简单例子

less 代码


```
.body{
  width:@test_width;
  height:@test_width;
  background-color: yellow;

  .border;

  left:100px;
}

//混合

.border{
  border:5px solid pink;
}
```

css代码

```
.body {
  width: 300px;
  height: 300px;
  background-color: yellow;
  border: 5px solid pink;
  left: 100px;
}
.border {
  border: 5px solid pink;
}
```

 
### 复杂例子

less代码 


```
//混合 - 可带参数的

.border_02(@border_width){
  border: solid yellow @border_width;
}

.test_hunhe{
  .border_02(30px);
}

//混合 - 默认带值
.border_03(@border_width:10px){
  border:solid green @border_width;
}

.test_hunhe_03{
  .border_03();
}

.test_hunhe_03{
  .border_03(50px);
}

//混合的例子

.border_radius(@radius:5px){
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  border-radius: @radius;
}

.radius_test{
  width:100px;
  height:40px;
  background-color: green;

  .border_radius();
}

.sanjiao{
  .triangle(top,100px);
}
```


css代码


```
.test_hunhe {
  border: solid yellow 30px;
}
.test_hunhe_03 {
  border: solid green 10px;
}
.test_hunhe_03 {
  border: solid green 50px;
}
.radius_test {
  width: 100px;
  height: 40px;
  background-color: green;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
.sanjiao {
  width: 0;
  height: 0;
  overflow: hidden;
  border-width: 10px;
  border-color: transparent transparent red transparent;
  border-style: dashed dashed solid dashed;
}
```

## 匹配模式
- 相当于JS中的if(但不完全是)
- 满足条件后才能匹配

less代码


```
//匹配模式
.triangle(top,@w:5px,@c:#ccc){
    border-width: @w;
    border-color: transparent transparent @c transparent;
    border-style: dashed dashed solid dashed;
}

.triangle(bottom,@w:5px,@c:#ccc){
  border-width: @w;
  border-color: @c transparent transparent transparent;
  border-style: solid dashed dashed dashed;
}

.triangle(left,@w:5px,@c:#ccc){
  border-width: @w;
  border-color: transparent @c transparent transparent;
  border-style: dashed solid dashed dashed;
}

.triangle(right,@w:5px,@c:#ccc){
  border-width:@w;
  border-color:transparent transparent transparent @c;
  border-style: dashed dashed dashed solid;
}
.sanjiao{
  .triangle(top,100px);
}

//匹配模式 - 定位
.pos(r){
  position:relative;
}

.pos(a){
  position:absolute;
}

.pos(f){
  position:fixed;
}

.pipe{
  width:200px;
  height:200px;
  background-color: green;
  .pos(r);
}
```

css代码


```
.sanjiao {
  border-width: 100px;
  border-color: transparent transparent #ccc transparent;
  border-style: dashed dashed solid dashed;
}
.pipe {
  width: 200px;
  height: 200px;
  background-color: green;
  position: relative;
}
```


## 运算
- 任何数字，颜色或者变量都可以参与运算，运算应该可以包裹在括号中。例如==：+ - * /==

less代码

```
//运算

@test_01:300px;

.box_02{
  width:@test_01 + 20;
}
```


css代码


```
.box_02 {
  width: 320px;
}
```

## 嵌套规则

- Less中最有意思的小东西
- 两种用法

（1）&对尾类使用
```hover```或者```
focus```

（2）对连接的使用```&-item```

---

less代码

```
//嵌套规则

/*
.list{}
.list li{}
.list a{}
.list span{}
*/

.list{
  width:600px;
  margin:30px auto;
  padding:0;
  list-style:none;

  li{
    height: 30px;
    line-height: 30px;
    background-color: pink;
    margin-bottom: 5px;
    padding:0 10px;
  }
  a{
    float:left;
    //&代表他的上一层选择器
    &:hover{
      color:red;
    }
  }
  span{
    float:right;
  }
}
```

css代码

```
/*
.list{}
.list li{}
.list a{}
.list span{}
*/
.list {
  width: 600px;
  margin: 30px auto;
  padding: 0;
  list-style: none;
}
.list li {
  height: 30px;
  line-height: 30px;
  background-color: pink;
  margin-bottom: 5px;
  padding: 0 10px;
}
.list a {
  float: left;
}
.list a:hover {
  color: red;
}
.list span {
  float: right;
}
```

## @arguments变量

- @arguments包含了所有传递进来的参数
- 如果你不想单独处理每一个参数的话就可以像这样写：


less代码

```
.border_arg(@w:30px,@c:red,@xx:solid){
  border:@arguments;  //相当于传入所有变量:border:@w @c @xx;
}

.test_arguments{
  .border_arg(40px);
}
```


css代码

```
.test_arguments {
  border: 40px red solid;
}
```


## 避免编译，！important以及总结

### 避免编译

- 有时候我们需要输出一些不正确的CSS语法或者使用一些Less不认识的专有语法。
- 要输出这样的值我们可以在字符串
前面加上一个```~```例如：```width:~'calc(100%-35)'```

less代码

```
//避免编译

.test_03{
  width:~'calc(300px - 30px)';
}
```

css代码

```
.test_03 {
  width: calc(300px - 30px);
}
```

### !important关键字

- 会为所有混合所带来的样式，添加上!important

less代码


```
//!important
.border_radius(@radius:5px){
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  border-radius: @radius;
}

.test_important{
  .border_radius()!important;
}
```


css代码


```
.test_important {
  -webkit-border-radius: 5px !important;
  -moz-border-radius: 5px !important;
  border-radius: 5px !important;
}
```

# 简单实战项目

![Snip20170721_54.png](https://i.loli.net/2017/07/21/5971ed640db2a.png)

[**项目代码**](https://github.com/liqilong199126/Less/tree/master/Less_demo)

# 更多

## Less中文网站

[**http://lesscss.net/**](http://lesscss.net/)

如果看不懂英文的，可以访问less中文旧版网站

[**http://old.lesscss.net/article/document.html**](http://old.lesscss.net/article/document.html)
