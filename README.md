# [Vue入门](https://www.bilibili.com/video/BV18E411a7mC)





## 第一章：介绍



### 1.概述

> **`Vue`**(谐音View)
>
> 是一套用于构建用户界面的**`渐进式框架`**
>
> 与其他大型框架不同的是，Vue被设计为可以自底向上逐层应用
>
> Vue的核心库只关心**`视图层`**
>
> 常见第三方库：
>
> + `vue-router`：路由
> + `vue-resources`：通信
> + `vuex`：管理



### 2.前端三要素

1. 结构层`HTML`
2. 表现层`CSS`
   + 代码复用层度低，重复选择器过多
3. 行为层`JavaScript`



### 3.前后端分离演变史

1. 后端以MVC为主的时代

+ ![缺点](https://i.imgur.com/LjV3lsc.png)
+ ![优点](https://i.imgur.com/Kj5WUE5.png)

+ ![缺点](https://i.imgur.com/B89WnHw.png)

2. 基于**`AJAX`**(异步JavaScript和XML)带来的`SPA`(**S**ingle **P**age **A**pplication)时代

+ ![优点](https://i.imgur.com/stive17.png)

+ ![缺点](https://i.imgur.com/s8Thdux.png)

3. 大前端时代

+ ![MV*](https://i.imgur.com/ruJzzGF.png)

+ *VM:ViewModel数据绑定*

4. NodeJS带来的全栈时代





## 第二章：MVVM模式和第一个Vue程序





### 1.MVVM模式的实现者

+ `Model`：模型层，在这里表示JavaScript对象
+ `View`：视图层，在这里表示DOM(HTML操作的元素)
+ `ViewModel`：连接视图和数据的中间件，Vue.js就是MVVM中的ViewModel层的实现者

> 在MVVM架构中，是不允许**数据**和**视图**直接通信的，只能通过ViewModel层来实现通信，而ViewModel就是定义了一个Observer观察者
>
> + ViewModel能够观察到数据的变化，并对视图对应的内容进行更新
> + ViewModel能够监听到视图的变化，并能够通知数据发生变化



### 2.第一个Vue程序

1. IntelliJ插件
2. NodeJS
3. Vue

```html
<!--demo_01.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>VueChapter1</title>
</head>
<body>
<h1>Vue_Learning_Demo1</h1>
<!--新建元素-->
<div id="app">
    {{message}}
</div>

<!--导入Vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        //绑定元素app
        el:"#app",
        data:{
            message:"Hello Vue Test"
        }
    })
</script>
</body>
</html>
```

测试双向绑定：数据的更新

+ ![Before](https://i.imgur.com/q71mWbe.png)

+ ![After](https://i.imgur.com/bERCQb5.png)





## 第三章：Vue基本语法



### 1.绑定数据

+ **`{{message}}`**等效于**`v-bind:title="message"`**，后者提高代码可读性。

+ **前缀"v-"的都是指令操作**



### 2.`IF-ELSE`

```html
<!--demo_02.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo2</title>
</head>
<body>
<div id="app">
<!--绑定boolean-->
    <!--当boolean为true-->
    <h1 v-if="boolean">The Value Is True</h1>
    <!--其他-->
    <h1 v-else>The Value Is False</h1>
</div>

<!--引入VueJS-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el:"#app",
        data:{
            boolean: true
        }
    });
</script>
</body>
</html>
```

![Before](https://i.imgur.com/IRJT1q6.png)

![After](https://i.imgur.com/zRceXxC.png)



### 3.`ELSE-IF`

同理于IF-ELSE



### 4.`FOR`

使用`v-for`遍历数组内容：`v-for="item in items"`

```html
<!--demo_03.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo3</title>
</head>
<body>
<div id="app">
    <!--遍历数组items中内容-->
    <li v-for="item in items">
        <!--指定内容message-->
        {{item.message}}
    </li>
    <br/>
    <li v-for="item in items">
        <!--指定内容text-->
        {{item.text}}
    </li>
</div>

<!--引入VueJS-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el:"#app",
        data:{
            items:[
                //定义数组内容"{键:值}"对
                {message: "message1"},
                {text: "plainText1"},
                {message: "message2"},
                {text: "plainText2"}
            ]
        }
    });
</script>
</body>
</html>
```



### 5.绑定事件*(事件肯定有方法)*

```html
<!--demo_04.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo4</title>
</head>
<body>
    
    
<div id="app">
    <!--使用v-on标签绑定事件-->
    <button v-on:click="showText">
        Click To Alert The Message
    </button>
</div>

<!--引入VueJS-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    //创建对象
    let vm = new Vue({
        el:"#app",
        data:{
            message: "This is a text"
        },
        //定义方法：注意methods单复数
        methods:{
            //定义event事件
            showText:function (event) {
                //this指向本对象
                alert(this.message);
            }
        }
    });
</script>
</body>
</html>
```





## 第四章：表单双绑、组件

### 1.概述



+ 什么是双向数据绑定？

  > 1. 当数据发生变化的时候，视图也发生变化；
  > 2. 当视图发生变化的时候，数据也会跟着同步变化；
  > 3. 一定是对于UI控件来说的，非UI控件不会涉及数据双向绑定
  > 4. 单向数据绑定是使用状态管理工具的前提：如果我们使用`vuex`，那么数据流也是单向的，这时就会和双向数据绑定有冲突。

+ 可以使用`v-model`在`<input>`、`<textarea>`、`<select>`元素上创建双向绑定，他会根据空间类型自动选取正确的方法来更新元素。`v-model`负责监听用户输入事件以更新数据，并对特殊场景进行处理。

示例：

```html
<!--demo_05.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo4</title>
</head>
<body>
<div id="app">
<!--Text-->
    Input Text Area:
    <label>
        <input type="text" v-model="InputText">
    </label>
    <!--展示内容-->
    {{InputText}}
    <br/>
<!--Textarea-->
    Input Textarea:
    <label>
        <textarea rows="3"  v-model="InputTextarea"></textarea>
    </label>
    <!--展示内容-->
    {{InputTextarea}}
    <br/>
<!--Radio-->
    Select Radio:
    <input type="radio" name="gender" value="Male" v-model="gender">Male
    <input type="radio" name="gender" value="Female" v-model="gender">Female
    <br/>
    <!--展示选项-->
    You've Selected : {{gender}}
    <br/>
<!--Drop List-->
    Select Drop List:
    <label>
        <select v-model="selected">
            <!--此处绑定后，如果需要设置默认选项必须把value置空，并且设置disabled-->
            <option disabled value="">Please Select</option>
            <option>Option#1</option>
            <option>Option#2</option>
            <option>Option#3</option>
            <option>Option#4</option>
        </select>
        <br/>
        <!--展示选项-->
        Your Selection is: {{selected}}
    </label>
</div>


<!--引入VueJS-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    //创建对象
    let vm = new Vue({
        el: "#app",
        data: {
            InputText: 'Default Text',
            InputTextarea: 'Default Textarea',
            gender:'',
            selected: ''
        }
    });
</script>
</body>
</html>
```



### 2.`<input>`

```html
<!--Text-->
    Input Text Area:
    <label>
        <input type="text" v-model="InputText">
    </label>
    <!--展示内容-->
    {{InputText}}
    <br/>
```

### 3.`<textarea>`

```html
<!--Textarea-->
    Input Textarea:
    <label>
        <textarea rows="3"  v-model="InputTextarea"></textarea>
    </label>
    <!--展示内容-->
    {{InputTextarea}}
    <br/>
```

### 4.`<select>`

```html
<!--Drop List-->
    Select Drop List:
    <label>
        <select v-model="selected">
            <!--此处绑定后，如果需要设置默认选项必须把value置空，并且设置disabled-->
            <option disabled value="">Please Select</option>
            <option>Option#1</option>
            <option>Option#2</option>
            <option>Option#3</option>
            <option>Option#4</option>
        </select>
        <br/>
        <!--展示选项-->
        Your Selection is: {{selected}}
    </label>
```

### 5.组件Component

概念：

+ 自定义合法标签
+ 可复用Vue实例，和JSTL的自定义标签、Thymeleaf的`th:fragment`等框架相似

```html
<!--demo_06.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo6</title>
</head>
<body>
<div id="app">

<!--当驼峰命名法时，例如firstComponent，第一个标签生效，第二个无效，aka.<first-component></first-component>，标签内不允许大写-->
<!--    <first-component></first-component>-->
<!--    <firstComponent></firstComponent>-->

<!--取items的值并将其赋值给item，通过itemPicker绑定组件模板-->
    <first-component v-for="item in items" v-bind:item-picker="item"></first-component>


</div>


<!--引入VueJS-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    //定义一个组件
    Vue.component("firstComponent" ,{
        // template: '<li>Hello</li>'

        //通过props取值
        props: ['itemPicker'],
        template: '<li>{{itemPicker}}</li>'


    });


    let vm = new Vue({
       el: '#app',
        data: {
           items: ["Item#1", "Item#2", "Item#3", "Item#4", "Item#5"]
        }
    });


</script>
</body>
</html>
```

+ 通过Vue.component()创建模板对象
+ 通过props来取值并且赋值给template
+ 遵循驼峰命名法的标签必须通过-来去除大写，标签内不允许任何大写



## 第五章：Axios异步通信



### 1.什么是Axios

​	可以用在浏览器和`NodeJS`的一部通信框架，主要作用就是实现`AJAX`异步通信，功能特点：

+ 从浏览器中创建`XMLHttpRequests`
+ 从node.js创建http请求
+ 支持Promise API [JS中链式编程]
+ 拦截请求和响应
+ 转换请求数据和响应数据
+ 取消请求
+ 自动转换JSON数据
+ 客户端支持防御XSRF(跨站请求伪造)

### 2.为什么要用Axios

`Vue.js`是一个视图层框架，严格遵守SoC(关注度分离原则)，所以`Vue.js`并不包含`AJAX`

的通信功能，为了解决通信问题，作者单独开发了`vue-resources`插件，不过在其2.0版本以后就停止维护，并推荐`Axios`框架。不推荐使用`jQuery`，因为它操作DOM太频繁。



### 3.第一个Axios应用程序

先在项目里模拟一段JSON数据，创建data.json数据内容如下

```json
//data.json
{
  "name": "Richard",
  "url": "https://google.com",
  "page": 1,
  "isNonProfit": true,
  "address": {
    "street": "fifth avenue",
    "city": "NewYork city",
    "country": "USA"
  },
  "link": [
    {
      "name": "demo#1",
      "url": "https://twitter.com"
    },
    {
      "name": "demo#2",
      "url": "https://facebook.com"
    },
    {
      "name": "demo#3",
      "url": "https://fast.com"
    }
  ]
}
```

放置在项目根目录下

**Vue生命周期**：红框内为钩子函数

![Vue生命周期](https://i.imgur.com/LhP8mtT.png)

```html
<!--demo_07.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo7</title>

    <!--手动解决闪烁而问题-->
    <style>
        [v-clock]{
            display: none;
        }
    </style>

</head>
<body>

<div id="vue" v-clock>
    <div>姓名：{{info.name}}</div>
    <div>街道：{{info.address.street}}</div>
    <div>城市：{{info.address.city}}</div>
    <div>国家：{{info.address.country}}</div>
    <div>是否盈利：{{info.isNonProfit}}</div>
    <a v-bind:href="info.url">链接</a>
</div>

<!--引入VueJS-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script type="text/javascript">
    let vm = new Vue({
        el: "#vue",
        data(){
            return {
                //return parameters must the same as java String
                info:{
                    name: null,
                    isNonProfit: null,
                    address:{
                        street: null,
                        city: null,
                        country:null
                    },
                    url:null
                }
            }
        },
        mounted(){//hook function,钩子函数，编译好的HTML挂载到页面完成后执行的事件钩子，此钩子函数一般会做一些AJAX请求获取数据，进行数据初始化， ATTN：mounted在整个实例中只执行一次
            axios.get('../data.json').then(response=>(this.info = response.data));
        }
    });
</script>
</body>
</html>
```

