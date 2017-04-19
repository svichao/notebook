#[百度前端技术学院笔记][1]
## [自定义checkbox、radio][2] ##

一. label标签
----------

####1. 概念：

  HTML <label>元素表示用户界面中项目的标题。 
 它通常关联一个控件，或者是将控件放置在label元素内，或者是用作其属性。这样的控制称作label元素的labeled control

####2. 用法：

**用法1：**

    <label>Click me <input type="text" id="User" name="Name" /></label>

**用法2：**

    <label for="User">Click me</label>
    <input type="text" id="User" name="Name" />

二. background-position属性
------------------------

####1. 概念：

background-position属性用来指定背景图片的初始位置；这个初始位置相对于background-origin定义的背景位置图层来说的

####2. 用法:

background-position:[position-x]，[position-y]
如果只有一个值被指定，则这个值就会默认设置背景图片位置中的水平方向，与此同时垂直方向的默认值被设置成50%。在关键词、百分比和数值混合指定的情况下，关键词 left 和 right 只能被指定水平方向的位置（第一个值）同时 top 和 bottom 只能被指定指定为垂直方向的值（第二个值）。同样，负数值是允许指定的。

三. 伪类和伪元素
---------

####1.概念：

**伪类**：存在的意义是为了通过选择器找到那些不存在于DOM树中的信息以及不能被常规CSS选择器获取到的信息。
伪类由一个冒号:开头，冒号后面是伪类的名称和包含在圆括号中的可选参数。
**常用伪类:**

    :active    向被激活的元素添加样式。    
    :focus    向拥有键盘输入焦点的元素添加样式。    
    :hover    当鼠标悬浮在元素上方时，向元素添加样式。    
    :link    向未被访问的链接添加样式。    
    :visited    向已被访问的链接添加样式。    
    :first-child    向元素的第一个子元素添加样式。    
    :checked 向选中的控件元素添加样式

伪元素:伪元素在DOM树中创建了一些抽象元素，这些抽象元素是不存在于文档语言里的（可以理解为html源码）；
注意:css3为了区分伪类和伪元素，规定伪类前面有一个冒号，伪元素前面有两个冒号
常用伪元素

    ::before 作为作用元素的第一个子节点插入dom中
    ::after 作为作用元素的最后一个子节点插入dom中
####2.区别与联系

**联系**：都是通过选择器为元素添加样式
**区别**:伪元素会创建一个元素，但不是真正的Html元素，伪类相当于为一个元素创建一个class样式

四、自定义控件的原理
----------

隐藏原生input标签，使用label，并且给之加样式来实现自定义控件
html：

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>自定义checkbox,radio样式</title>
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <div id='wrap'>
            <h2>伪元素实现：</h2>
            <div class="checkbox">
                <input type="checkbox" name="" id="checkBox" class="checkBox">
                <label for="checkBox"></label>
            </div>
            <div class="radio">
                <input type="radio" name="sex"  id="radioBox" class="radios">
                <label for="radioBox"></label>
                <input type="radio" name="sex"  id="radioBox1" class="radios">
                <label for="radioBox1"></label>
            </div>
            <h2>雪碧图实现：</h2>
            <div class="checkbox">
                <input type="checkbox" name="" id="checkBox_sprit" class="checkBox_sprit">
                <label for="checkBox_sprit"></label>
            </div>
            <div class="radio">
                <input type="radio" name="sex1"  id="radioBox_sprit" class=" radioBox_sprit">
                <label for="radioBox_sprit"></label>
                <input type="radio" name="sex1"  id="radioBox1_sprit" class=" radioBox_sprit">
                <label for="radioBox1_sprit"></label>
            </div>
        </div>
    </body>
    </html>

 - 伪元素方法实现

使用:checked伪类和::after伪元素,当控件选中时添加伪元素到label标签中：
css:

    .checkbox{
      margin-bottom: 30px;
      font-weight: 700;
    }
    .checkBox+label,.radios+label{
      width:16px;
      height: 16px;
      border:1px solid #d9d9d9;
      display: -webkit-flex;
      display:flex;
    }
    .checkBox:checked+label,.radios:checked+label{
       border:1px solid #d73d32;
       font-weight: 700;
    }
    .checkBox:checked+label::after,.radios:checked+label::after{
      margin: auto;
      content: '2714';
      color: red;
      width:8px;
      height:8px;
      line-height: 8px;
      text-align: center;
      font-size: 12px;
    }
    input{
      margin:0;
      display: none;
    }
    
    /* radio */
    .radio{
      display: -webkit-flex;
      display: flex;
      width: 50px;
      -webkit-justify-content: space-between;
      justify-content: space-between;
    }
    .radios+label{
      border-radius: 50%;
    }
    .radios:checked+label::after{
      border-radius: 50%;
      width:8px;
      height:8px;
      line-height: 8px;
      content: ' ';
      background: #d73d32;
    }

[效果展示][3]
[源码地址][4]

 - 雪碧图实现方法:

给label加一个背景图片，并通过设置选中状态时的background-position属性
css:

    .checkBox_sprit+label,.radioBox_sprit+label{
      width: 16px;
      height:16px;
      border:none;
      display: inline-block;
      background:url('bg.png') no-repeat;
    }
    .checkBox_sprit+label{
      background-position:-25px -32px;
    }
    .radioBox_sprit+label{
      background-position: -24px -10px;
    }
    .checkBox_sprit:checked+label{
      background-position: -60px -32px;
    }
    .radioBox_sprit:checked+label{
      background-position: -59px -10px;
    }

效果展示
源码地址

五. css雪碧图和css伪元素两种方法的比较
-----------------------

使用伪元素可以不用图片，这样就减少了http的收发次数，提高了网络性能。
使用css雪碧图，可以使还原度更加精确，代码量减少。


  [1]: http://ife.baidu.com/note/list?isElite=1
  [2]: http://ife.baidu.com/note/detail/id/28
  [3]: https://elva2596.github.io/ife-tasks/task-1/index.html
  [4]: https://github.com/elva2596/elva2596.github.io/tree/master/ife-tasks/task-1