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





## 第六章：计算属性、内容分发、自定义事件

### 1.什么是计算属性

> ​	计算属性的重点突出在`属性`两字上(名词)，首先它是个`属性`，其次它有`计算`的能力(动词)，这里的`计算`就是个函数；简单点说，他就是一个能够将计算结果缓存起来的属性(将行为转化成了静态的属性)，仅此而而已；可以想象为缓存。

+ 也就是说，当缓存刷新时，计算结果也将刷新，如果参数是动态的话，那计算结果很有可能和原来的不同

```html
<!--demo_08.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue_Learning_Demo8</title>
</head>
<body>
<h1>Vue_Learning_Demo8</h1>
<div id="app">
    <p>{{currentTime1()}}</p>
    <p>{{currentTime2}}</p>
</div>

<!--导入Vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    let vm = new Vue({
        el:"#app",
        data: {
            message: "Hello Vue"
        },
        //可以重名，重名后只调用方法；
        //注意：此处定义出来的是方法
        methods: {
            currentTime1: function () {
                return Date.now(); //return current timestamp
            }
            // returnBothTime: function () {
            //     console.log(alert("currentTime1 is:" + this.currentTime1() + "\ncurrentTime2 is:" + this.currentTime2));
            // }
        },
        //此处返回的是属性
        computed: {
            currentTime2: function(){
                //当内容变化后将刷新缓存
                this.message;
                //return computed value
                //返回计算出来的结果
                return Date.now();
            }
        }
    })
</script>
</body>
</html>
```



+ 在console里调用currentTime1()时，结果会刷新：![currentTime1()](https://i.imgur.com/vp8Mzji.png)

+ 在console里调用currentTime2时，结果不刷新，因为已经作为属性写入缓存：![currentTime2](https://i.imgur.com/3KYtcap.png)

+ 通过改变data中的值刷新缓存之后：![Cache Flushed](https://i.imgur.com/QTfh9YR.png)

**说明**：

+ methods：定义方法，调用方法使用currentTime1()，需要带括号。
+ computed：定义计算属性，调用属性使用currentTime2，不需要带括号；this.message是为了能够让currentTime2观察到数据变化而变化
+ 如果在方法中的值发生了变化，则缓存就会刷新！可以在console使用`vm.message="Change Value"`，改变下数据的值，再次测试观察效果！

**结论**：

​		调用方法时，每次都需要进行计算，既然有计算过程则必定产生系统开销，那如果这个结果是不经常变化的呢？此时就可以考虑将这个结果缓存起来，采用计算属性可以很方便的做到这一点，**计算属性的主要特征就是为了将不经常变化的计算结果进行缓存，以节约系统开销。**





### 2.内容分发

​		在`Vue.js`中我们使用`<slot>`元素作为承载分发内容的出口，作者称其为`插槽`，可以应用在组合组件的场景中。



**实现**：

​		制作一个待办事项组件(todo)，该组件由代办标题和代办内容组成，但这三个组件又是**相互独立**的，该如何操作呢？

​			**第一步**：定义一个待办事项的组件：

```html
<div id="app">
    <todo>
	</todo>
</div>
<script type="text/javascript">
    Vue.component("todo", {
        //反斜杠代替换行\
        //todo包含:todo-title,todo-items，slot中放置todo-title,todo-items
        template://name属性绑定插槽
        '<div>\
            <div>todo_list</div>\
                <ul>\
                    <li>learning Java</li>
                </ul>\
        </div>'
    });
</script>
```

​			**第二步**：我们需要让待办事项的标题和值实现动态绑定，怎么做呢？我们可以先留出一个插槽；

1. 添加`<slot>`插槽

```javascript
Vue.component("todo", {
        //反斜杠代替换行\
        //todo包含:todo-title,todo-items，slot中放置todo-title,todo-items
        template://name属性绑定插槽
        '<div>\
            <slot name="todo-title"></slot>\
                <ul>\
                    <slot name="todo-items"></slot>\
                </ul>\
        </div>'
    });
```

2. 定义一个名为`todo-title`的待办事项标题组件和`todo-items`的待办事项内容组件

```javascript
Vue.component('todo-title', {
    props: ['title'],
    template: '<div>{{title}}</div>'
});
```

```javascript
Vue.component('todo-items', {
    props: ['item', 'index'],
    template: '<li>{{index + 1}}---{{item}}</li>'
});
```

3. 实例化Vue并初始化数据

```javascript
let vm = new Vue({
    el: '#vue',
    data: {
        todoItems: ['Item#1', 'Item#2', 'Item#3', 'Item#4']
    }
});
```

4. 将这些值通过插槽插入

```html
<div id="vue">
    <todo>
        <todo-title slot="todo-title" title="Vue.js Learning"></todo-title>
        <todo-items slot="todo-items" v-for="(item, index) in todoItems" 
                    v-bind:item="item" v-bind:index="index"></todo-items>
    </todo>
</div>
```

至此，todo-title和todo-items组件分别被分发到了todo组件的todo-title和todo-items插槽中。

### 3.自定义事件

​		通过以上代码不难发现，数据项在Vue的实例中，但删除操作要在组件中完成，那么组件如何才能删除Vue实例中的数据呢？此时就涉及到了参数传递与事件分发了，Vue为我们提供了自定义事件的功能很好的帮助我们解决了这个问题；使用this.$emit('自定义事件名', 参数)，操作过程如下：

1. 在vue实例中，增加了methods对象并定义一个名为removeTodoItems的方法

```javascript
let vm = new Vue({
    el: '#vue',
    data: {
        title: 'Vue.js Learning',
        todoItems: ['Item#1','Item#2','Item#3','Item#4','Item#5','Item#6']
    },
    methods: {
        removeItem: function (index) {
            console.log(this.todoItems[index] + ' deleted successfully! ');
            this.todoItems.splice(index, 1);
        }
    }
});
```

2. 修改todo-items待办内容的组件代码，增加一个删除按钮，并且绑定事件

```javascript
Vue.component("todo-items",{
    props: ['item', 'index'],
    //1、先将item和index传递，将事件绑定，
    //此处onclick绑定方法名
    //注意样式设计
    template:
        '<tr>\
            <td>\
                {{item}}\
            </td>\
            <td>\
                {{index}}\
            </td>\
            <td>\
                <button v-on:click="rm_itm">\
                    Delete\
                </button>\
            </td>\
        </tr>',
    methods: {
        //方法名大小写敏感
        rm_itm: function (index) {
    	//此处do_remove为自定义事件
            this.$emit('do_remove', index);
        }
    }
});
```

3. 修改todo-items待办内容组件的HTML代码，增加一个自定义事件，比如叫do_remove，可以和组件的方法进行绑定，然后绑定到vue的方法中！

```html
<!--创建key属性让其有唯一ID，Vue 为了节省资源重复利用已有 DOM 节点，要求开发者给列表中的元素加上唯一的 key，在排序之类的操作时，不需要销毁创建新节点。-->
<!--可通过样式包裹slot标签-->
<table>
    <tr>
        <th>项目</th>
        <th>索引</th>
        <th>删除</th>
    </tr>
    <todo-items slot="todo-items" v-for="(item, index) of todoItems"
                v-bind:item="item" v-bind:key="index" v-bind:index="index" v-on:do_remove="removeItem(index)"></todo-items>
</table>
```

4. 逻辑理解

![逻辑理解](https://i.imgur.com/GuwaBcN.png)





## #入门小结

​		**核心：数据驱动，组件化**

​		**优点：借鉴了AngulaJS的模块化开发和React的虚拟DOM，虚拟DOM就是把DOM操作放到内存中执行；**

### 		**常用的属性：**

+ `v-if`
+ `v-else-if`
+ `v-else`
+ `v-for`
+ `v-on`绑定事件，简写`@`
+ `v-model`数据双向绑定
+ `v-bind`给组件绑定参数，简写`:`



### 		**组件化：**

+ 组合组件slot插槽
+ 组件内部绑定事件需要使用到的`this.$emit('事件名', 参数)`
+ 计算属性的特色，缓存计算数据

​		**遵循SoC关注度分离原则，Vue是纯粹的视图框架，并不包含像AJAX之类的通信功能，为了解决通信问题，需要使用Axios框架做异步通信。**



### 		补充说明：

​		Vue的开发都是要基于NodeJS，实际开发采用vue-cli脚手架开发，vue-router路由，vuex做状态管理，Vue UI界面通常使用ElementUI(饿了么出品)，或者ICE(阿里巴巴出品)来快速搭建前端项目。





# Vue



## 第一章：第一个vue-cli项目





### 1.什么是vue-cli

​	vue-cli官方提供的一个脚手架，用于快速生成一个vue项目模板；

​	预先定义好的目录结构及基础代码，就好比创建`maven`项目时可以选择创建一个骨架项目，这个骨架项目就是脚手架，更快速开发。



​		**主要的功能**：

+ 统一的目录结构
+ 本地调试
+ 热部署
+ 单元测试
+ 集成打包上线



### 2.需要的环境

+ NodeJS 配置环境
+ git



**NodeJS淘宝镜像加速**

```bash
# -g全局安装

npm install cnpm -g

# 或使用如下语句解决速度慢问题 (Recommanded)
npm install --register=https://registery.npm.taobao.org
```



**修改NPM默认下载安装位置**

````bash
#更改全局安装路径

npm config set prefix "/ur/custom/path/node_global" 

#更改缓存路径

npm config set cache "/ur/custom/path/node_cache"
````





**安装`vue-cli`**

```bash
npm install vue-cli

# 测试安装是否成功
# 查看当前可以基于那些模板创建vue应用程序，通常使用 webpack

vue list
```

![vue-list](https://i.imgur.com/lOZlffs.png)





### 3.第一个vue-cli程序



1. 创建一个Vue项目，建立空文件夹
2. 创建一个基于webpack模板的vue应用程序(在当前目录下打开终端)

```bash
# 此处 $ProjectName 是项目名称

vue init webpack $ProjectName
```

3. 一路选择`No`即可
4. 说明：
   + Project Name：项目名称
   + Project description：项目描述
   + Author：项目作者
   + install vue-router：是否安装`vue-router`
   + USE ESLint to lint your code：是否使用`ESLint`做代码检查
   + Set up unit tests：单元测试相关
   + Setup e2e tests with Nightwatch：单元测试相关
   + Should we run npm install for you after the project has been created：创建完成后直接初始化
5. 初始化并运行

```bash
cd $ProjectName

npm install # 通过package.json中的版本描述进行安装，相当于pom.xml

npm run dev
```

