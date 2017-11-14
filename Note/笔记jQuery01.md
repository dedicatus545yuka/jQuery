### 初识jQuery
1. 什么是`jQuery`？
- jQuery是一个JavaScript函数库 - window.$ = window.jQuery = jQuery
- jQuery是一个轻量级的"写的少，做的多"的JavaScript库。
- jQuery库包含以下功能：
    - html的元素操作
    - html dom遍历和修改
    - js特效和动画效果
    - css操作
    - html事件操作
    - ajax异步请求方式
2. 为什么使用`jQuery`?
- 目前jQuery兼容于所有主流浏览器
- jQuery是目前最流行的JS框架，而且提供了大量的扩展

3. jQuery 版本 2,版本 3 不支持 IE6，7，8 浏览器。
如果需要支持 IE6/7/8，那么请选择1.10
你还可以通过条件注释在使用 IE6/7/8 时只包含进1.10。 
```js
<!--[if lt IE 9]>
    <script src="jquery-1.9.0.js"></script>
<![endif]-->
<!--[if gte IE 9]><!-->
    <script src="jquery-2.0.0.js"></script>
<!--<![endif]-->
```

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>01_初识jQuery</title>

  <!--
  方式一: 使用原生JS实现功能
  -->
  <script type="text/javascript">
    window.onload = function () {
      var btn = document.getElementById('btn1')
      btn.onclick = function () {
        alert(document.getElementById('username').value)
      }
    }
  </script>
  <!--
  方式二: 使用jQuery实现功能
    1. 引入jQuery库
      * 本地引入
      * 远程引入
    2. 使用jQuery函数和jQuery对象编码
  -->
  <script type="text/javascript" src="js/jquery-1.10.1.js"></script>
  <script type="text/javascript">
    $(function () {
        $('#btn2').click(function () {
            alert($('#username').val());// alert - 页面弹出提示框的方式显示内容
        })
    })
  </script>
</head>
<body>
<!--
需求: 点击"确定"按钮, 提示输入的值
-->

用户名: <input type="text" id="username">
<button id="btn1">确定(原生版)</button>
<button id="btn2">确定(jQuery版)</button>
</body>

</html>
```
### jQuery的两把利器
1. jQuery核心函数
  * 简称: jQuery函数($/jQuery)
  * jQuery库向外直接暴露的就是$/jQuery
  * 引入jQuery库后, 直接使用$即可
    * 当函数用: $(xxx)
    * 当对象用: $.xxx()
2. jQuery核心对象
  * 简称: jQuery对象
  * 得到jQuery对象: 执行jQuery函数返回的就是jQuery对象
  * 使用jQuery对象: $obj.xxx()
```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>jQuery的二把利器</title>
</head>
<body>
<button>测试</button>
<script type="text/javascript" src="js/jquery-1.10.1.js"></script>
<script type="text/javascript">

  console.log(typeof $)   //$是一个function
  console.log($ === jQuery) //true  $与jQuery等同
  console.log($ === window.$) //true  $是一个全局函数

  console.log(typeof $()) //"object"  这个对象就是jQuery对象

  $('button').click(function () {
    alert(this.innerHTML) // 这里的this 指向被jQuery封装的DOM对象
  })
</script>
</body>
</html>
``` 
### jQuery的核心函数  
1. 作为一般函数调用: $(param)
  1). 参数为函数 : 当DOM加载完成后，执行此回调函数
  2). 参数为选择器字符串: 查找所有匹配的标签, 并将它们封装成jQuery对象
  3). 参数为DOM对象: 将dom对象封装成jQuery对象
  4). 参数为html标签字符串 (用得少): 创建标签对象并封装成jQuery对象
2. 作为对象使用: $.xxx()
  1). $.each() : 隐式遍历数组
  2). $.trim() : 去除两端的空格
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery核心函数</title>
    <script type="text/javascript" src="js/jquery-1.10.1.js"></script>
</head>
<body>

    <div>
        <button id="btn">测试</button><br>
        <input type="text" name="massage01"><br>
        <input type="text" name="massage02"><br>
    </div>

    <script>
            $(function () {
                // 需求1. 点击按钮: 显示按钮的文本, 显示一个新的输入框
                    $('#btn').click(function () {
//                        alert($('#btn').html());
                        $('<input type="text" name="massage03"><br>').appendTo('div');
                    });
                // 需求2. 遍历输出数组中所有元素值
                    var arr = [1,2,3,4];
                    $.each(arr,function (index,itemValue) {
//                        console.log(index,itemValue);
                    });
                // 需求3. 去掉"  my atguigu  "两端的空格
                    var str = "  my atguigu  ";
                    console.log(str.trim() === "my atguigu");// true
                    console.log($.trim(str) === "my atguigu");// true
            })
    </script>
</body>
</html>
```
### jQuery对象
1. jQuery对象是一个包含所有匹配的任意多个dom元素的伪数组（类数组）对象
2. 基本行为
  * size()/length: 包含的DOM元素个数
  * [index]/get(index): 得到对应位置的DOM元素
  * each(): 遍历包含的所有DOM元素
  * index(): 得到在所在兄弟元素中的下标
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery对象</title>
</head>
<body>
<button>测试一</button>
<button>测试二</button>
<button class="btn3">测试三</button>
<button>测试四</button>

<script type="text/javascript" src="js/jquery-1.10.1.js"></script>
<script>
    $(function () {
//        需求1. 统计一共有多少个按钮
        console.log($('button').length,$('button').size());// 4 , 4
//        需求2. 取出第2个button的文本
        console.log($('button')[1].innerHTML);// 测试二
        console.log($('button').get(1).innerHTML); // 测试二
//        需求3. 输出所有button标签的文本
        $('button').each(function () {
            console.log(this.innerHTML);
        })
//        需求4. 输出'测试三'按钮是所有按钮中的第几个
        console.log($('.btn3').index());
    })
</script>
</body>
</html>
```
### 基本选择器
1. 是什么?
  - 有特定格式的字符串
2. 作用
  - 用来查找特定页面元素
3. 基本选择器
  - #id : id选择器
  - element : 元素选择器
  - .class : 属性选择器
  - *: 任意标签
  - selector1,selector2,selectorN : 取多个选择器的并集(组合选择器)
  - selector1selector2selectorN : 取多个选择器的交集(相交选择器)
```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>05_基本选择器</title>
</head>

<body>
<div id="div1" class="box">div1(class="box")</div>
<div id="div2" class="box">div2(class="box")</div>
<div id="div3">div3</div>
<span class="box">span(class="box")</span>

<br>
<ul>
  <li>AAAAA</li>
  <li title="hello">BBBBB(title="hello")</li>
  <li class="box">CCCCC(class="box")</li>
  <li title="hello">DDDDDD(title="hello")</li>
</ul>

<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  $(function () {
// 1. 选择id为div1的元素
    // $('#div1').css('background', 'red')
// 2. 选择所有的div元素
    // $('div').css('background', 'red')
// 3. 选择所有class属性为box的元素
    // $('.box').css('background', 'red')
// 4. 选择所有的div和span元素
    // $('div,span').css('background', 'red')
// 5. 选择所有class属性为box的div元素
    // $('div.box').css('background', 'red')  //不能写.boxdiv
  })
</script>
</body>

</html>
```
### 层次选择器
层次选择器: 查找子元素, 后代元素, 兄弟元素的选择器
1. ancestor descendant（中间是一空格） -  父 空格 子
- 在给定的祖先元素下匹配所有的后代元素
2. parent>child
- 在给定的父元素下匹配所有的子元素
3. prev+next
- 匹配所有紧接在 prev 元素后的 next 元素
4. prev~siblings
- 匹配 prev 元素之后的所有 siblings 元素
```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>06_层次选择器</title>
</head>

<body>

<ul>
  <li>AAAAA</li>
  <li class="box">CCCCC</li>
  <li title="hello"><span>BBBBB</span></li>
  <li title="hello"><span>DDDD</span></li>
  <span>EEEEE</span>
</ul>

<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  $(function () {
//1. 选中ul下所有的的span
    //$('ul span').css('background', 'red')
//2. 选中ul下所有的子元素span
    //$('ul>span').css('background', 'red')
//3. 选中class为box的下一个li
    // $('.box+li').css('background', 'red')
//4. 选中ul下的class为box的元素后面的所有兄弟元素
    $('ul .box~*').css('background', 'red')
  })
</script>
</body>
</html>
```
### 过滤选择器
- 在原有选择器匹配的元素中进一步进行过滤的选择器
  * 基本
  * 内容
  * 可见性
  * 属性
```html<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>07_过滤选择器</title>
</head>

<body>
<div id="div1" class="box">class为box的div1</div>
<div id="div2" class="box">class为box的div2</div>
<div id="div3">div3</div>
<span class="box">class为box的span</span>
<br/>
<ul>
  <li>AAAAA</li>
  <li title="hello">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two">BBBBB</li>
  <li style="display:none">我本来是隐藏的</li>
</ul>

<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">

  $(function () {
//1. 选择第一个div
    //$('div:first').css('background', 'red')
//2. 选择最后一个class为box的元素
    //$('.box:last').css('background', 'red')
//3. 选择所有class属性不为box的div
    //$('div:not(.box)').css('background', 'red')
//4. 选择第二个和第三个li元素
    //$('li:gt(0):lt(2)').css('background', 'red') //索引起始位置发生变化，重新开始计算
    //$('li:lt(3):gt(0)').css('background', 'red') //正确索引位置
//5. 选择内容为BBBBB的li
    //$('li:contains(BBBBB)').css('background', 'red')
//6. 选择隐藏的li
    //$('li:hidden ').show()
//7. 选择有title属性的li元素
    //$('li[title]').css('background', 'red')
//8. 选择所有属性title为hello的li元素
    //$('li[title=hello]').css('background', 'red')
  })
</script>
</body>

</html>
```
### 表单选择器
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>08_表单选择器</title>
</head>

<body>
<form style="text-align: center">
  用户名: <input type="text"/><br>
  密 码: <input type="password"/><br>
  爱 好:
  <input type="checkbox" checked="checked"/>篮球
  <input type="checkbox" checked="checked"/>足球
  <input type="checkbox" checked="checked"/>羽毛球 <br>
  性 别:
  <input type="radio" name="sex" value='male'/>男
  <input type="radio" name="sex" value='female'/>女<br>
  邮 箱: <input type="text" name="email" disabled="disabled"/><br>
  所在地:
  <select>
    <option value="1">北京</option>
    <option value="2" selected="selected">天津</option>
    <option value="3">河北</option>
  </select><br>
  <input type="submit" value="提交"/>
</form>
<!--
表单选择器
  1). 表单
  2). 表单对象属性
-->
<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  
  $(function () {
//1. 选择不可用的文本输入框
    //$(':input:disabled').css('background', 'red')
//2. 显示选择爱好 的个数
    //console.log($(':checkbox:checked').length)
//3. 显示选择的城市名称
    console.log($('select>option:selected').html())
    console.log($('select').val())  //得到的是选择的option的value
  })
</script>
</body>
</html>
```
### 工具方法
1. $.each(): 遍历数组或对象中的数据
2. $.trim(): 去除字符串两边的空格
3. $.type(obj): 得到数据的类型
4. $.isArray(obj): 判断是否是数组
5. $.isFunction(obj): 判断是否是函数
6. $.parseJSON(json) : 解析json字符串转换为js对象/数组     

json整体就2种类型:     
1. json对象 : {key1:value1 , key2:value2}
2. json数组: [value1, value2]
3. key只能是字符串
4. value的类型:
     - number
     - string
     - boolean
     - null
     - []
     - {}
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>09_$工具方法</title>
</head>
<body>

<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">

  //1. $.each(): 遍历数组或对象中的数据
  var person = {
    name: 'tom',
    age: 12
  }
  $.each(person, function (key, value) {
    console.log(key, value)
  })

  //2. $.trim(): 去除字符串两边的空格

  //3. $.type(obj): 得到数据的类型
  console.log($.type($) === "function")

  //4. $.isArray(obj): 判断是否是数组
  console.log($.isArray($()))  //false
  console.log($.isArray([]))  //true

  //5. $.isFunction(obj): 判断是否是函数
  console.log($.isFunction($)) //true
  console.log($.isFunction($())) //false

  //6. $.parseJSON(json) : 解析json字符串转换为js对象/数组
  
  var json = '{"username":"jack", "age" : 12}'
  console.log($.parseJSON(json))  //js对象
  json = '[{"username":"jack", "age" : 12},{"username":"Tom", "age" : 13}]'
  console.log($.parseJSON(json)) //js数组

</script>
</body>
</html>
```
### 属性
1. 操作任意属性
   attr()
   removeAttr()
   prop()
2. 操作class属性
   addClass()
   removeClass()
3. 操作HTML代码/文本/值
   html()
   val()
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>10_属性</title>
</head>
<body>

<div id="div1" class="box" title="one">class为box的div1</div>
<div id="div2" class="box" title="two">class为box的div2</div>
<div id="div3">div3</div>
<span class="box">class为box的span</span>
<br/>
<ul>
  <li>AAAAA</li>
  <li title="hello" class="box2">BBBBB</li>
  <li class="box">CCCCC</li>
  <li title="hello">DDDDDD</li>
  <li title="two"><span>BBBBB</span></li>
</ul>

<input type="text" name="username" value="guiguClass"/>
<br>
<input type="checkbox">
<input type="checkbox">
<br>
<button>选中</button>
<button>不选中</button>

<script src="js/jquery-1.10.1.js" type="text/javascript"></script>
<script type="text/javascript">
  $(function () {
//  1. 读取第一个div的title属性
    // console.log($('div:first').attr('title'))
//  2. 给所有的div设置name属性(value为atguigu)
    // $('div').attr('name', 'atguigu')
//  3. 移除所有div的title属性
    // $('div').removeAttr('title')
//  4. 给所有的div设置class='guiguClass'
    // $('div').attr('class', 'guiguClass')
//  5. 给所有的div添加class值(abc)
    // $('div').addClass('abc')
//  6. 移除所有div的guiguClass的class
    // $('div').removeClass('guiguClass')
//  7. 得到最后一个li的标签体文本
    // console.log($('li:last').html())
//  8. 设置第一个li的标签体为"<h1>mmmmmmmmm</h1>"
    // $('li:first').html('<h1>mmmmmmmmm</h1>')
//  9. 得到输入框中的value值
    // console.log($(':text').val())
//  10. 将输入框的值设置为atguigu
    // $(':text').val('atguigu')
//  11. 点击'全选'按钮实现全选
    $('button:first').click(function () {
      $(':checkbox').prop('checked', true)
    })
//  12. 点击'全不选'按钮实现全不选
    $('button:last').click(function () {
      $(':checkbox').prop('checked', false)
    })
  })

</script>
</body>
</html>
```
