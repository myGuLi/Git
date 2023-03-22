# vue2

## 一、什么是vue

一套用于构建用户界面的渐进式js框架，vue可以自底向上逐层的应用。简单应用:只需一个轻量小巧的核心库。复杂应用：可以引入各式各样的vue插件

 

### 1.1 vue的特点

* 采用组件化模式，提高代码复用率、且让代码更好维护
* 声明式编码，让编码人员无需直接操作dom，提高开发效率
* 使用虚拟dom+优秀的diff算法，尽量复用dom节点

### 1.2初始vue

* 想让vue工作，就需要创建一个Vue实例，且要穿放入一个配置对象

* root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法

* root容器里的代码被称为【Vue模板】

* Vue实例和容器是一一对应的

* 真是开发中只有一个Vue实例，并且会配合着组件一起使用

* {{XXX}}中的XXX重要些js表达式，且XXX可以自动读取到data中的所有属性

* 一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新

  

  

  ```
  <body>
      <div id="root">
          <h1>hello {{name}}</h1>
      </div>
      <script type="text/javascript">
          Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
  
          //创建Vue实例
          const vm = new Vue({
              el: '#root', 
              //el:element的缩写，用于指定当前Vue实例为那个容器服务，值通常为css选择器字符串
              //el:document.getElementById('root')这种写法也可以
              data: {
                  //data中用于存储数据，数据供el所制定的容器去使用，值暂时先写成一个对象
                  name: '谷俊丽'
              }
  
          })
      </script>
  </body>
  ```
  
  注意：区分js表达式和js代码(js语句)
  
  ​	1、表达式：一个表达式会生成一个值，可以放在任何一个需要值的地方
  
  ​		(1) a
  
  ​		(2)a+b
  
  ​		(3)dem0(1)
  
  ​		(4)三元表达式
  
  ​	2、代码
  
  ​	(1)if(){}
  
  ​	(2)for(){}

## 二.模板语法-两大类



###  2.1 插值语法

​	功能：用于解析标签体内容

​	写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性

### 2.2指令语法

​	功能：用于解析标签(包括：标签属性、标签体内容、绑定事件)

​	举例：v-bind:href='xxx'或简写为:href='xxx'，xxx同样要写js表达式。且可以直接读取到data中的所有属性

​	备注：Vue中有很多指令，且形式都是：v-??

 ```
<div id="root">
        <h1>差值语法</h1>
        <h3>你好，{{name}}</h3>
        <hr>
        <h1>指令语法</h1>
        <a v-bind:href="url">尚硅谷</a>
        <!-- v-bind:href:把url转换为js表达式，即把url看成一个变量。'v-bind:'可以简写为'：' -->
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',

            data: {

                name: '谷俊丽',
                url: 'http://www.atguigu.com'
            }

        })
    </script>
 ```

![1664676060328](C:\Users\Tom\AppData\Local\Temp\1664676060328.png)

## 三.Vue数据绑定

### 3.1 单行数据绑定v-bind

>  ** 数据只能从data流向页面** 

```
<div id="root">
        单向数据绑定：<input type="text" :value="name">
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                name: '谷俊丽'
            }

        })
    </script>
```

![1664676972520](C:\Users\Tom\AppData\Local\Temp\1664676972520.png)

### 3.2 双向数据绑定v-model

* v-model:只能应用在表单类元素（输入类元素上，如 input ,select等）,需要有value

* v-model:value 可以简写v-model 因为v-model默认收集的就是value值

  





```
<div id="root">
        双向数据绑定：<input type="text" v-model:value="name">
        //简写形式：双向数据绑定：<input type="text" v-model="name">
        
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                name: '谷俊丽'
            }
        })
    </script>
```



![1664677227885](C:\Users\Tom\AppData\Local\Temp\1664677227885.png)





## 四.el与data的两种写法

### 4.1  el的两种方法

#### 4.1.1方法一

```
<div id="root">
        <h1>你好，{{name }} </h1>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                name: '谷粒'
            }
        })
    </script>
```

#### 4.1.2 方法二

```
<div id="root">
        <h1>你好，{{name }} </h1>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false
        var vm = new Vue({
            data: {
                name: '谷粒'
            }
        })
        vm.$mount('#root')
    </script>
```

### 4.2 data的两种形式

#### 4.2.1 方法一:对象式

```
new Vue({
            el: '#root',
            data: {
                name: '谷粒'
            }
        })
```

#### 4.2.2 方法二：函数式（组件时必须使用）

```
new Vue({
            el: '#root',
           data:function(){//函数必须要有返回值
          console.log(this)//此时的this是Vue实例对象！！！注意，这里的函数必须是普通函数，不是箭头函数
 						 //箭头函数的this是全局的window
               return{
                   name:'谷粒'
               }
           }
        })

```

简写形式：

```
new Vue({
            el: '#root',
            data(){
              return{
                    name: '谷粒'
              }
            }
        })
```

## 五.MVVM

* M,模型(Model),对应data数据

* V,视图(View),模板

* VM,视图模型(ViewModel),Vue实例

* data中所有的属性，最后都出现在了vm 上

* vm身上所有的属性及vue原型上所有的属性，在Vue模板中都可以直接使用

  

  ​	<img src="C:\Users\Tom\Desktop\前端笔记\Snipaste_2023-03-09_19-32-26.png" alt="Snipaste_2023-03-09_19-32-26" style="zoom: 67%;" />

## 六，Object.defineProperty()：

定义新属性或修改原有的属性

Object.defineProperty(obj,prop,descriptor)

obj:目标对象

prop:需定义或修改的属性名字

descriptor:，目标属性所拥有的特性

```
descriptor:以对象形式{}书写
value:设置属性的值，默认为undefined
writable:值是否可以重写，true|false,默认为false
enumerable:值是否可以被枚举，true|false,默认为false
configurable:值是否可以被删除或是否可以再次修改特性true|false,默认为false

```



```
<script>
var obj={
    id:1,
    pname:'小米'
}
Object.defineProperty(obj,'num',{
    value:1000//设置num的值为1000
})//若目标对象中没有num，则添加num属性
若没有特殊指明，num不能被枚举
</script>
```

```
<script>
let n=18
var obj={
    id:1,
    pname:'小米'
}
Object.defineProperty(obj,'num',{
  
  //当有人读取obj的num属性时，get函数(getter)就会被调用，且返回值就是num的值
  //可以简写get(){}
  get：function(){
      return n//这个时候，只要有人读取了num这个属性，num的值就是n的最新值
  }
   //当有人修改obj的num属性时，set函数(setter)就会被调用，且会收到修改的具体值value
  set(value){
      n=value
  }
})
</script>
```





## 七.数据代理

定义:通过一个对象，代理对另一个对象中枢性的操作(读/写)

```
 <script type="text/javascript">
        let obj = {
            x: 100
        }
        let obj2 = {
            y: 200
        }
        Object.defineProperty(obj2, 'x', {
            get() {
                return obj.x
            },
            set(value) {
                obj.x = value
            }
        })
    </script>
```

### 7.1 Vue中的数据代理

1、Vue中，通过vm对象代理data对象中的属性操作

2、好处：更加方便操作data中的数据

3、基本原理

​	①通过Object.defineProperty()把data对象总所有的属性添加到vm上

​	②为每一个添加到vm上的属性添加getter/setter，

​	③在getter/setter内部操作data中对应的属性



<img src="C:\Users\Tom\Desktop\前端笔记\Snipaste_2023-03-09_20-32-37.png" alt="Snipaste_2023-03-09_20-32-37" style="zoom:60%;" />



<img src="C:\Users\Tom\Desktop\前端笔记\Snipaste_2023-03-09_20-34-35.png" alt="Snipaste_2023-03-09_20-34-35" style="zoom:60%;" />



## 八.事件处理

```
<body>
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <button v-on:click="showInfo">点我提示信息</button>
        <button @click="showInfo">点我提示信息</button>//简写形式
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                name: '尚硅谷'
            },
            methods: {
                showInfo() { //可以传进参数，参数是实例对象e
                    console.log(this); //此处的this是vm
                    alert('你好')
                }
            },
        })
    </script>
</body>
```

可以传参：

```
<body>
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <!-- <button v-on:click="showInfo">点我提示信息</button> -->
        <button @click="showInfo1">点我提示信息1</button>//这个按钮绑定showInfo 函数
        <button @click="showInfo2($event,66)">点我提示信息2</button>//这个按钮绑定showInfo 函数
        
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                name: '尚硅谷'
            },
            methods: {
                showInfo1() { //可以传进参数
                    console.log(this); //此处的this是vm
                    alert('你好')
                },
                showInfo2(e, num) {
                    console.log(num);//66
                    alert('你好')
                }
            },
        })
    </script>
</body>
```

* 使用v-on:xxx或@xxx绑定事件，其中xxx是事件名

* 事件的回调需要配置在method对象中，最终会在vm上

* methods中的配置函数不能使箭头函数，否则this就不是vm而是window

* methods中配置的函数，都是被vue所管理的函数，this的指向是vm或组件实例对象

* @click="demo"和@click="demo($event)"效果一致，但后者可以传参,

* $event是鼠标事件

  

## 九.事件修饰符

Vue中的事件修饰符

1、prevent:阻止默认事件(常用)

2、stop：阻止事件冒泡(常用)

3、once：事件只触发一次

4、self:只有event.target是当前操作的元素时，才触发事件

### 1.阻止默认事件方法一

```
<body>
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <a href="#" @click="showInfo($event)">点击</a>
        
        <div class="demo1" @click="showInfo">
            <button @click="showInfo">点点点</button>
        </div>
    </div>

    <script type="text/javascript">
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                name: '尚硅谷'
            },
            methods: {
                showInfo(e) {
                    alert('nihao')
                    e.preventDefault();//阻止默认事件
                    e.stopPropagation();//阻止冒泡事件

                }
            },
        })
    </script>
</body>
```

### 2.阻止默认事件方法二

```
<a href="#" @click.prevent="showInfo($event)">点击</a>//阻止默认事件
----------------------------------------------------
<div class="demo1" @click="showInfo">
            <button @click.stop="showInfo">点点点</button>//阻止冒泡事件
        </div>
----------------------------------------------------
   <button @click.once="showInfo">点点点</button>//事件只触发一次，第二次点击就不会触发事件
```

页面滚动事件：$@scroll='demo'(滚轮滚动触发)  @wheel='demo'(鼠标滚动触发)$

### 3.补充

可以先阻止冒泡后阻止默认事件,也可以先阻止默认事件后阻止冒泡，效果相同

```
 <div class="demo1" @click="showInfo">
            <a  href='xxx' @click.stop.prevent="showInfo">点点点</a>
        </div>
```

```
 <div class="demo1" @click="showInfo">
            <a  href='xxx' @click.prevent.stop="showInfo">点点点</a>
        </div>
```



## 十.键盘事件

当按下enter键是，打印出input表单的value值

1、普通做法：

```

<body>
    <div id="root">
        <h2>欢迎来到{{name}}学习</h2>
        <input type="text" placeholder="按下回车同时输入" @keyup="showInfo">//enter是别名
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                name: '尚硅谷'
            },
            methods: {
                showInfo(e) {
                if (e.keyCode !== 13) //13是回车键的ASCAII码
                        return
                    console.log(e.target.value);
                }
            },
        })
    </script>
</body>
```

### 1.Vue中常用的别名

* 回车：enter
* 删除:delete (捕获"删除"键和”退格键“)
* 退出：esc
* 空格：space
* 换行：tab//不适用keyup,必须适用keydown
* 上：up
* 下：down
* 左:left
* 右：right

2.使用别名：

```
 <input type="text" placeholder="按下回车同时输入" @keyup.enter="showInfo">
 //enter是别名,可以在按下enter键时触发事件，调用showInfo函数
 
------------------------------------------------------------------------------------ 
 methods: {
                showInfo(e) {
     				console.log(e.target.value);
                }
            },
```

### 2.Vue中未提供别名的按键：

可以使用按键原始的key值绑定，但注意要有的要短横线命名，如caps-lock 

### 3.系统修饰键

ctrl，alt，shift，meta(win)

​	(1)可以配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发

​	(2)配合keydown：正常触发事件

拓展：只有Ctrl+y时，才会触发事件

```
 <input type="text" placeholder="按下回车同时输入" @keyup.ctrl.y="showInfo">
 											//y可以修改
```

### 4.其他方式

1、配合keyCode(不推荐)

2、Vue.config.keyCodes.自定义键名=键码，可以去定制按键别名



## 十一.计算属性与监视

### * 前言-------姓名案例

#### 插值语法实现

```

    <div id="root">
        姓: <input type="text" v-model:value='firstName'> <br>
        名: <input type="text" v-model:value='lastName'> <br>
        姓名： <span>{{firstName.slice(0,3)}} - {{lastName}}</span>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',

            data: {

                firstName: '张',
                lastName: '三'
            },
        })
    </script>
```



#### methods实现方式

```
<body>
    <div id="root">
        姓: <input type="text" v-model:value='firstName'> <br>
        名: <input type="text" v-model:value='lastName'> <br>
        姓名： <span>{{fullName()}}</span><br><br>
       <!-- //调用fullName()函数的返回值 -->
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                firstName: '张',
                lastName: '三'
            },
            methods: {
                fullName() {
                    return this.firstName + '-' + this.lastName //this是vue实例
                }
            },
        })
    </script>
</body>
```

### 1. 计算属性-computed

```
计算属性：
1、定义：要用的属性不存在，要通过已有的属性计算得来
2、原理：低层借助了Object.definepropery方法提供的getter和setter
3、get函数什么时候执行？
	（1）初次读取时会执行一次
	（2）当依赖的数据发生改变时会被再次调用
4、优势：与methods实现相比，内部有缓存机制（复用），效率跟高，调试方便
5、备注：
  （1）计算属性最终会出现在vm上，直接读取使用即可
  （2）如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生变化
```



```
<body>
    <div id="root">
        姓: <input type="text" v-model:value='firstName'> <br>
        名: <input type="text" v-model:value='lastName'> <br>
        姓名： <span>{{fullName}}</span><br><br>//直接引用
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                firstName: '张',
                lastName: '三'
            },
            computed: {
                fullName: {
                    //get有什么作用？当有人读取fullName时，get就会被调用，且返回值就为fullName的值 
                    get() {
                        return this.firstName + '-' + this.lastName //this是vue 实例
                    },
                    set(value) { //当fullName被修改时
                        const arr = value.split('-')
                        this.firstName = arr[0]
                        this.lastName = arr[1]
                    }
                }
            }
        })
    </script>
</body>
```

简写形式

```
 computed: {
                // fullName: {
                //     get() {
                //         return this.firstName + '-' + this.lastName //this是vue 实例
                //     },
                //     set(value) { //当fullName被修改时,调用set
                //         const arr = value.split('-')
                //         this.firstName = arr[0]
                //         this.lastName = arr[1]
                //     }
                // }

                //简写 在只获取数据的情况下
                fullName: function () { //fuction就是get函数
                    return this.firstName + '-' + this.lastName
                }
            }
```



### 2、监视属性

#### （1）、方法一

```
<div id="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="changeWeather">切换天气</button>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                isHot: true
            },
            computed: {
                info() {
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods: {
                changeWeather() { 
                    this.isHot = !this.isHot
                }
            },
            watch: {
                isHot: {
                    //handler什么时候调用？ 当isHot发生改变时 
                    handler(newValue, oldValue) {
                    }
                }
            },
        })
    </script>
```

#### （2）、方法二

```
 vm.$watch('isHot,', {

            isHot: {
                immediate: true, //初始化时让handler调用一下
                //handler什么时候调用？ 当isHot发生改变时
                handler(newValue, oldValue) {
                    console.log('isHot被修改了', newValue, oldValue);
                }
            }
        })
```

​                                            

### 3 深度监视

````
 <div id="root">
        <h3>a的值是:{{numbers.a}} </h3>
        <button @click="add">点我让a+1</button>
    </div>

    <script type="text/javascript">
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                numbers: {
                    a: 1,
                    b: 1
                }
            },
            methods: {
                add() {
                    this.numbers.a++
                }
            },
            // 深度监视：（1）Vue中的watch默认不检测对象内部值的改变（一层）
            //(2) 配置deep:true可以检测对象内部值改变（多层）

            watch: {
                'numbers.a': { //监视多级结构中某个属性的变化
                    deep: true, //监视多级结构中所有属性的变化
                    handler() {
                        console.log('a变化了');
                    }
                }
            }
        })
    </script>
````

//正常写法

```
 watch: {
                 //正常写法
                isHot: {
                     immediate: true, //初始化时让handler调用一下
                     //handler什么时候调用？ 当isHot发生改变时
                    handler(newValue, oldValue) {
                         console.log('isHot被修改了', newValue, oldValue);
                     }
                 }

                //简写  函数当handler用
                isHot() {
                    console.log('isHot被修改了', newValue, oldValue);
                }
            }
```

```
 vm.$watch('isHot', {
            // immediate: true, //初始化时让handler调用一下
            //handler什么时候调用？ 当isHot发生改变时
            handler(newValue, oldValue) {
                console.log('isHot被修改了', newValue, oldValue);
            }
        })
```



//简写

```
 //简写  函数当handler用
       watch: {
                isHot() {
                    console.log('isHot被修改了', newValue, oldValue);
                }
```

```
 vm.$watch('isHot', function (newValue, oldValue) {
            console.log('isHot被修改了', newValue, oldValue);
        })
```

### 4、watch对比computed

```
1、computed能完成的功能，watch都可以完成
2、watch能完成的功能，computed不一定能完成，例如watch可以进行异步操作
watch: {
                firstName(newValue) {
                    setInterval(() => {
                        this.fullName = newValue + '-' + this.lastName
                    }, 1000);
                },
                lastName(newValue) {
                    this.fullName = this.firstName + '-' + newValue
                }
            }


两个重要的小原则
   1、所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm
   2、所有不被Vue所管理的函数（定时器回调函数、Ajax的回调函数等最好写成箭头函数）,这样this的指向才是vm
```



#### 1 、watch修改姓名案例

```
 <div id="root">
        姓: <input type="text" v-model:value='firstName'> <br>
        名: <input type="text" v-model:value='lastName'> <br>
        姓名： <span>{{fullName}}</span><br><br>

    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                firstName: '张',
                lastName: '三',
                fullName: '张-三',
                x: 1,
                y: 2

            },
            computed: {
                a() {
                    return this.x + this.y
                }
            },
            watch: {
                firstName(newValue) {
                    this.fullName = newValue + '-' + this.lastName
                },
                lastName(newValue) {
                    this.fullName = this.firstName + '-' + newValue
                }
            }

        })
    </script>
```

### 十二、绑定class样式、style样式

```
<body>
    <div id="root">
        <!-- 绑定class样式————字符串写法，适用于：样式的类名不确定，需要动态指定 -->
        <div class="basic normal" :class="mood" @click="changeMood">{{name}}</div>

        <!-- 绑定class样式———数组写法，适用于：要绑定的样式个数不确定，名字也不确定 -->
        <div class="basic" :class="classArr">{{name}}</div>
        <!-- 绑定class样式————对象写法，适用于：要绑定的样式个数确定，名字也确定,动态决定用不用 -->
        <div class="basic" :class='classObj'>{{name}}</div>
        
      //绑定style写法
        <div class="basic" :style="styleObj">{{name}}</div>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',

            data: {
                name: '谷俊丽',
                mood: 'normal',
                classArr: ['s1', 's2', 's3'],
                //vm.arr.shfit():移除数组元素   vm.arr.push() 添加数组元素
                classObj: {
                    s1: false,
                    s2: false
                },
              styleObj:{
              fontSize:'40px'
              }
            },
            methods: {
                changeMood() {
                    const arr = ['happy', 'sad']
                    const i = Math.floor(Math.random() * 3) //[0,1)
                    this.mood = arr[i]

                }
            },

        })
    </script>
</body>

```

### 十三、条件渲染

```
<div id="root">
        <!-- v-show='false'时 底层控制display的属性值 结构还在 可以获取到元素-->
        <!-- <h2 v-show="false">欢迎来到{{尚硅谷}}</h2> -->
        <!-- <h2 v-show="1===3">欢迎来到{{尚硅谷}}</h2> -->
        <!-- 1===3的值是false -->
        <!-- <h2 v-show="a">欢迎来到{{尚硅谷}}</h2> -->


        <!-- 用v-if做条件渲染值为false时 整个dom结构都被移除，不能获取元素 -->
        <!-- <h2 v-if="false">欢迎来到{{尚硅谷}}</h2> -->
        

        <!-- 互动小案例 -->
        <!-- //切换频繁的用v-show -->
        <h2>当前n的值是{{n}}</h2>
        <button @click="n++">点我n加1</button>
        <div v-show="n===1">a</div>
        <div v-show="n===2">b</div>
        <div v-show="n===3">c</div>
        
        
         <!-- 互动小案例 -->
        <!-- v-else和v-else-if -->
        <h2>当前n的值是{{n}}</h2>
        <button @click="n++">点我n加1</button>
        <div v-if="n===1">a</div>
        <div v-else-if="n===2">b</div>
        <div v-else-if="n===3">c</div>
        <div v-else>haha</div>
        
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false
        const vm = new Vue({
            el: "#root",
            data: {
                name: '尚硅谷',
                n: 0
            },
            // a: false


        })
    </script>
```

### 十四、列表渲染

#### 1、基本列表

```
<body>
    <div id="root">
        <ul>
           <li v-for="p in persons" :key="p.id"> {{p.name}}-{{p.age}}</li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例
        const vm = new Vue({
            el: '#root',

            data: {
                persons: [
                    {id: '001',name: '张三',age: 18},
                    {id: '002',name: '李四',age: 13},
                    {id: '003',name: '王五',age: 12}
                ]
            }

        })
    </script>
</body>
```



```
 <li v-for="(p,index) in persons" :key="index"> {{p}}----{{index}}</li>
  <li v-for="(p,index)  of  persons" :key="index"> {{p}}----{{index}}</li>
  两种写法
 p是数组对象
 index是数组对象的id值
```

#### 2、key的作用与原理



```
1、虚拟DOM中key的作用：
	key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据新数据生成新的虚拟DOM，随后Vue进行新虚拟DOM与旧虚拟DOM的差异比较。
2、对比原则：
	（1）旧虚拟DOM中找到了与新虚拟DOM相同的key：
		①	旧虚拟DOM中内容没有变，直接使用之前的真实DOM
		②若旧虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM
	（2）旧虚拟dom中未找到与新虚拟DOM相同的key
		创建新的真实DOM，随后渲染到页面
3、用index作为key可能会引发的问题：
		若对数据进行：逆序添加、逆序删除等破坏顺序操作：会产生没有必要的真实DOM更新，界面效果没问题，但效率低
		
		（2）、如果结构中还包含输入类DOM：会产生错误DOM更新==界面有问题
4、开发中如何选择key？：
	（1）、最好使用每条数据的唯一标识作为key，比如ID、手机号、身份证号、学号等唯一值
	（2）、如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲列表用于展示，使用index是没有问题的。
	
	
```

#### 3、列表过滤

```
 <div id="root">
        <h2>人员列表</h2>
        <input type="text" placeholder="请输入名字" v-model="keyWord">
        <ul>
            <li v-for="(p,index) of filPersons" :key="index">
                {{p.name}}----{{p.age}}----{{p.sex}}
            </li>

        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。

        //创建Vue实例,用watch实现
        // // const vm = new Vue({
        // el: '#root',

        //     data: {
        //         keyWord: '',
        //         persons: [{
        //                 id: '001',
        //                 name: '马冬梅',
        //                 age: 18,
        //                 sex: '女'
        //             },
        //             {
        //                 id: '002',
        //                 name: '周冬雨',
        //                 age: 13,
        //                 sex: '女'
        //             },
        //             {
        //                 id: '003',
        //                 name: '周杰伦',
        //                 age: 12,
        //                 sex: '男'
        //             },
        //             {
        //                 id: '0004',
        //                 name: '温兆伦',
        //                 age: 20,
        //                 sex: '男  '

        //             }

        //         ],
        //         filPersons: []
        //     },
        //     watch: {
        //         keyWord: {
        //             immediate: true,
        //             handler(val) {

        //                 this.filPersons = this.persons.filter((p) => {
        //                     return p.name.indexOf(val) !== -1
        //                     //若str='abc' str.indexOf(' ')==0 str.indexOF('a')==0
        //                 })
        //             }
        //         }
        //     }

        // })

        new Vue({
            el: '#root',
            data: {
                keyWord: '',
                persons: [{
                        id: '001',
                        name: '马冬梅',
                        age: 18,
                        sex: '女'
                    },
                    {
                        id: '002',
                        name: '周冬雨',
                        age: 13,
                        sex: '女'
                    },
                    {
                        id: '003',
                        name: '周杰伦',
                        age: 12,
                        sex: '男'
                    },
                    {
                        id: '0004',
                        name: '温兆伦',
                        age: 20,
                        sex: '男 '

                    }

                ]

            },
            computed: {
                filPersons() {
                    return this.persons.filter((p) => {
                        return p.name.indexOf(this.keyWord) !== -1
                    })
                }
            }

        })
    </script>
</body>
```



#### 4、列表排序

```
<div id="root">
        <h2>列表排序</h2>
        <button @click="sortType=2">年龄升序</button>
        <button @click="sortType=1">年龄降序</button>
        <button @click="sortType=0">原顺序</button>
        <input type="text" placeholder="请输入名字" v-model="keyWord">
        <ul>
            <li v-for="(p,index) of filPersons" :key="id">
                {{p.name}}----{{p.age}}----{{p.sex}}
            </li>
        </ul>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        new Vue({
            el: '#root',
            data: {
                keyWord: '',
                sortType: 0, //0代表原顺序，1代表降序、2升序
                persons: [
                    {id: '001', name: '马冬梅', age: 28,sex: '女' },
                    {id: '002',name: '周冬雨',age: 13, sex: '女'},
                    {id: '003', name: '周杰伦',age: 12, sex: '男'},
                    {id: '004',name: '温兆伦',age: 20,sex: '男 ' }
                ]

            },
            computed: {
                filPersons() {
                    const arr = this.persons.filter((p) => {
                        return p.name.indexOf(this.keyWord) !== -1
                    })
                    //判断一下是否需要排序
                    if (this.sortType) {
                        arr.sort((p1, p2) => {
                            return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age //降序后减前
                        })
                    }
                    return arr
                }
            }

        })
    </script>
```



### 十五、数据监视

#### 1、模拟数据检测

```
 <script type="text/javascript">
        //准备一个vm实例对象
        let vm = {}
        vm._data = data = obs
        let data = {
            name: '尚硅谷',
        }
        //创建一个监视的实例对象，用于监视data中属性的变化
        function Observe(obj) {
            //汇总对象中所有的属性形成一个数组
            Object.keys(obj)
            //遍历
            keys.forEach(k => {
                Object.defineProperty(this, k, {
                    get() {
                        return obj[k]
                    },
                    set(val) {
                        obj[k] = val
                    }
                })
            });

        }
    </script>
```

#### 2、总结Vue监视数据

1、Vue会监视data中所有层级的数据

2、如何检测对象中的数据？

​	通过getter实现监视，且在new Vue时就传入要监视的数据

​	（1）、对象中后追加的属性Vue默认不做响应式处理

​	（2）、如需给后添加的属性做响应式，则需使用以下api

​				Vue.set(target,properyName/index/,value)

​				或vm.$set(target,propertyName/index,value)

3、如何检测数组中的数据

​		通过包裹数数组更新元素的方法实现，本质就是做了两件事：

​		（1） 、调用原生对应的方法对数组进行更新

​		（2）、重新解析模板，进而更新页面

4、在Vue修改数组中的某个元素，一定要用如下方法

​	（1）、使用这些api:push ()、pop(),shift(),unshift(),splice(),sort(),reverse(),

​		（2）、Vue.set()或vm.$set()

特别注意：Vue.set()和vm.$set(),不能给vm或vm的跟数据对象添加属性                                                                                                                                                                                     

## 

### 十六 、收集表单数据

```
<div id="root">

        <form action="" @submit.prevent="demo">
            账号：<input type="text" id="demo" v-model.trim="account"><br><br>
            密码：<input type="password" v-model="password"><br><br>
            年龄：<input type="number" v-model.number="age"><br><br>
            性别：
            男：<input type="radio" name="sex" value="female" v-model="sex">
            女：<input type="radio" name="sex" value="female" v-model="sex"><br><br>
            爱好：
            学习： <input type="checkbox" v-model="hobby" value="学习">
            打游戏:<input type="checkbox" v-model="hobby" value="打游戏">
            吃饭: <input type="checkbox" v-model="hobby" value="吃饭"><br><br>
            所属校区：
            <select name="" id="" v-model="city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shangahi">上海</option>
                <option value="shenzhen">深圳</option>
            </select><br><br>
            其他信息
            <textarea name="" id="" cols="30" rows="10" v-model.lazy="other"></textarea><br>

            <input type="checkbox">阅读并接受<a href="javascript;">《用户协议》</a><br>
            <button>提交</button>

        </form>
    </div>

    <script type="text/javascript">
        Vue.config.productionTip = false
        const vm = new Vue({
            el: '#root',
            data: {
                account: '',
                password: '',
                sex: 'female',
                hobby: [],
                city: '',
                other: '',
                age: 15,


            },
            methods: {
                demo() {
                    alert(1)
                }
            },
        })
    </script>
```



#### 1、 v-model 的三个修饰符：

​	lazy：失去焦点再收集字符

​	number：输入字符串转为有效数字

​	trim:输入首尾空格过滤

#### 2、注意一

 <input type='checkbox'>

​		（1）、没有配置input的value值，那么收集的就是checked值

​		（2）、配置input的value值：

​				①v-model的初始值是非数组，那么收集的就是checked

​				②初始值是数组：那么手机的就是value组成的数组

#### 3、注意二

若<input type='text'>，则v-model收集的是value值，用户输入的就是value值

#### 4、注意三

若<input type='radio'>，则v-model收集的是value值，需要给标签配置value值



### 十七、 过滤器

Vue.js 允许你自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：**双花括号插值和 v-bind 表达式** (后者从 2.1.0+ 开始支持)。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符号指示：

```
<!-- 在双花括号中 -->
{{ message | capitalize }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>
```

你可以在一个组件的选项中定义本地的过滤器：

```
filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
```

或者在创建 Vue 实例之前全局定义过滤器：

```
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})

new Vue({
  // ...
})
```

### 十八、内置指令

#### 1、v-text

* 作用：向其所在的节点中渲染文本内容

* 与插值语法的区别：v-text会替换掉节点中的内容，{{xxx}}不会

  ```
  <div id="root">
          <div v-text="name">  </div>   //浏览器显示谷俊丽
           <div v-text="msg"> </div>		//浏览器显示<h2>你好<h2>
      </div>
      <script type="text/javascript">
          Vue.config.productionTip = false;
          const vm = new Vue({
              el: '#root',
              data: {
                  name: '谷俊丽',
                  msg: '<h2>你好<h2>'
              }
  
          })
      </script>
  ```

  

  

  

#### 2、v-html

更新元素的 [innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)。

`v-html` 的内容直接作为普通 HTML 插入—— Vue 模板语法是不会被解析的。如果你发现自己正打算用 `v-html` 来编写模板，不如重新想想怎么使用组件来代替。

`在你的站点上动态渲染任意的 HTML 是非常危险的，因为它很容易导致 [XSS 攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。请只对可信内容使用 HTML 插值，**绝不要**将用户提供的内容作为插值`

#### 3、v-cloak

用于隐藏尚未完成编译的 DOM 模板。

当使用直接在 DOM 中书写的模板时，可能会出现一种叫做“未编译模板闪现”的情况：用户可能先看到的是还没编译完成的双大括号标签，直到挂载的组件将它们替换为实际渲染的内容。

`v-cloak` 会保留在所绑定的元素上，直到相关组件实例被挂载后才移除。配合像 `[v-cloak] { display: none }` 这样的 CSS 规则，它可以在组件编译完毕前隐藏原始模板。配合css使用可以解决网速慢是页面展示出{{xxx}}的问题。

#### 4、v-once

仅渲染元素和组件一次，并跳过之后的更新。

* v-once 所在的节点在初次动态渲染后，就视为静态内容了
* 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能

 #### 5、v-pre

`跳过该元素及其所有子元素的编译。`

元素内具有 `v-pre`，所有 Vue 模板语法都会被保留并按原样渲染。最常见的用例就是显示原始双大括号标签及内容。

<span v-pre>{{ this will not be compiled }}</span>

* 跳过其所在节点的解析
* 可以利用它跳过没有指令语法、没有使用插值语法的节点，会加快编译



### 十九、自定义指令

#### 例--->函数式和对象式

```
 <!-- 需求一：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍
        需求二：定义一个v-fbind指令，和v-bind功能类似，但可以让其绑定的input元素默认获取焦点
    -->
    <div id="root">
        <h2>当前n的值是： <span v-text="n"></span></h2>
        <h2>放大后10倍n的值是： <span v-big="n"></span></h2>
        <button @click="n++">n+1 </button>
        <hr>
        <input type="text" v-fbind:value="n">
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            data: {
                name: '谷俊丽',
                n: 1
            },
            directives: {
                // big函数何时会被调用？1、指令与元素成功绑定时。
                //                    2、指令所在的模板被重新解析时
                big: function (element, binding) { //big(){}
                    element.innerText = binding.value * 10
                },
                fbind: {
                    bind(element, binding) {
                        //指令与元素成功绑定时，调用bind 函数
                        element.value = binding.value
                    },
                    inserted(element, binding) {
                        //指令所在元素被插入页面时，调用inserted函数
                        element.focus()
                    },
                    update(element, binding) {
                        //指令所在的模板(root)被重新解析时，调用update函数
                        element.value = binding.value
                    }
                }
            }
        })
    </script>
```

#### 总结

一、语法定义

​	（1）、局部指令

​	new Vue({

​		directives:{指令名：配置对象}

​		})

或

​	new Vue({

​		directives:{指令名：函数}

​		})

​	(2)、全局指令

​	Vue.directive(执行名，配置对象)

​	或

​	Vue.directive(指令名，函数)



二、配置对象中常用的3个回调

* bind:指令与元素成功绑定时

* inserted：指令所在元素被插入页面时调用

* update：指令所在模板结构被重新解析时调用

  

三、备注：

* 指令定义时不加v-
* 指令名如果时多个单词，要使用kebab-case命名方式，不能用大小驼峰连写形式，并在定义函数时，指令名需要加单引号。

### 二十、生命周期

* 又名：声明周期回调函数、声明周期函数、声明周期钩子
* 是Vue在关键时刻帮我们调用的一些特殊名称的函数
* 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
* 声明周期函数中的this指向的组件实例对象

```
   <div id="root">
        <h2 :style={opacity:opacity}>欢迎学习Vue</h2>
    </div>
    <script type="text/javascript">
      Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        new Vue({
            el: '#root',
            data: {
                opacity: 1
            },
            methods: {},
            //挂载
            mounted() {
                //vue完成模板解析，并把初识的真实的DOM元素放入页面后调用mounted
                setInterval(() => {
                    this.opacity -= 0.01
                    if (this.opacity <= 0) this.opacity = 1
                }, 20);
            },

        })
   
```



### 二十一、非单文件组

```
<div id="root">

        <!-- <h2>学校名称：{{schName}}</h2>
        <h2>学校地址：{{address}}</h2> -->

        <!-- step3:编写组件标签 -->
        <school></school>
        <hr>
        <!-- <h2>学生姓名：{{stuName}}</h2>
        <h2>学生年级：{{age}}</h2> -->
        <student></student>

    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false; //设置为 false 以阻止 vue 在启动时在控制台生成生产提示。
        //step1:创建组组件
        //创建school组件
        const school = Vue.extend({
            template: `
        <div>
            <h2>学校名称：{{schName}}</h2>
            <h2>学校地址：{{address}}</h2>
        </div>
            `,
            //el:'#root',
            //组件定义时一定不要写el配置项，因为最终所有的组件都要被一个vm管理，有vm决定服务于哪个容器
            data() {
                return {
                    schName: '尚硅谷',
                    address: '北京'
                };
            },
        })


        //创建student组件
        const student = Vue.extend({
            template: `
            <div>
            <h2>学生姓名：{{stuName}}</h2>
            <h2>学生年级：{{age}}</h2>
            </div>
            `,
            data() {
                return {
                    stuName: '谷俊丽',
                    age: 18
                };
            },
        })

        //创建Vue实例
        const vm = new Vue({
            el: '#root',
            //step2:注册组件（局部注册）
            data: {
                msg: '初识组件'
            },
            components: {
                school: school,
                student: student
            }

        })
    </script>
```

#### 1、Vue使用组件的三大步骤

+ 定义组件（创造组件）

+ 注册组件（局部注册和全局注册）

+ 使用组件（写组件标签）

   

#### 2、组件的几个注意事项

* 1、关于组件名：

  * 一个单词构成：
    * 第一种写法（首字母小写）：school
    * 第二种写法（首字母大写）：School

  * 多个单词组成：

    * 第一种写法（kebab-case）：my-school,在component中是'my-school'

    * 第二种写法(CamelCase)    ：MySchool（需要用到Vue脚手架支持）

      

  * 备注

    * （1）、组件名尽可能回避HTML中已有的元素名称，如 h2/H2

    * （2）、可以使用Name配置项制定组件在开发者工具中呈现的名字

      

* 2、关于组件标签：

  * 第一种写法：<School></School>

  * 第二种写法：<school/>

  * 不适用脚手架，<school/>会导致后续组件不能渲染

    

* 3、一个简写方式：

  ```
   const school = Vue.extend({options}) 可简写 const school={options}
  ```

  

 #### 3、VueComponent构造函数

关于VueComponent：

* school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的

* 我们只需要写<school></school>,Vue 解析时会自动帮我们创建school组件实例对象。

  即Vue会帮我们执行new VueComponent(options) 

* 特别注意，每次调用Vue.extend,返回的都是一个全新的VueComponent

* 关于this指向

  * 组件配置中：

    * data函数，methods中的函数，watch中的函数，computed中的函数，他们的this都是：VueComponent实例对象

      

  * new Vue()配置中：
    
    * data函数，methods中的函数，watch中的函数，computed中的函数，他们的this都是：Vue实例对象

#### 4、一个重要的内置关系

VueComponent.prototype. __ proto __===Vue.prototype



可以让组件实例对象（vc）可以访问到Vue原型上的属性、方法。

### 二十一、vue脚手架

   中文官网:https://cli.vuejs.org/zh

​	Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统

#### 1、安装

win+R，打开点到cmd，运行：`npm install -g @vue/cli` 或者`yarn global add @vue/cli`

安装之后，你就可以在命令行中访问 `vue` 命令。你可以通过简单运行 `vue`，看看是否展示出了一份所有可用命令的帮助信息，来验证它是否安装成功。

你还可以用这个命令来检查其版本是否正确：`vue --version`

#### 2、升级

如需升级全局的 Vue CLI 包，请运行：

```
npm update -g @vue/cli

# 或者
yarn global upgrade --latest @vue/cli
```

#### 3、创建一个项目

* 1、选择要项目要存放的磁盘:

  ` cd + 存放目录` 如：C:\Users\Tom>cd desktop

  

* 2、运行以下命令来创建一个新项目：

​	`vue create hello-world`

* 3、选择`defaule(bable eslint) `

#### 4、拉取 2.x 模板 (旧版本)[#](https://cli.vuejs.org/zh/guide/creating-a-project.html#拉取-2-x-模板-旧版本)

Vue CLI >= 3 和旧版使用了相同的 `vue` 命令，所以 Vue CLI 2 (`vue-cli`) 被覆盖了。如果你仍然需要使用旧版本的 `vue init` 功能，你可以全局安装一个桥接工具：

```
npm install -g @vue/cli-init
# `vue init` 的运行效果将会跟 `vue-cli@2.x` 相同
vue init webpack my-project
```



### 二十二、分析脚手架结构

一个插件：vuetur

#### 1、VueSchool.vue

```
<template>
    <!-- 组件的结构 -->
    <div class="demo">
            <h2>学校名称：{{SchName}}</h2>
            <h2>学校地址：{{SchAddress}}</h2>
            <button @click="show">点我提示学校名</button>
    </div>
</template>

<script>
// 组件交互的相关代码（数据、方法等）
export default {
    name: 'VueSchool',
    data() {
        return {
            SchName: '尚硅谷',
            SchAddress:'北京'
        };
    },

    mounted() {
        
    },

    methods: {
        show() {
            alert(this.SchName)
        }
    },
}
</script>

<style lang="scss" scoped>
// 组件的样式
.demo{
    background-color:pink;
}
</style>
```

#### 2、VueStudent.vue

```
<template>
    <div class="stu">
        <h2>学生姓名：{{Name}}</h2>
        <h2>学生年级：{{Age}}</h2>
    </div>
</template>

<script>

export default {
    name: 'VueStudent',
    data() {
        return {
             Name: '谷俊丽',
             Age: 18
        };
    },
};
</script>

<style lang="scss" scoped>
.stu{
    background-color: red;
}
</style>
```



其它组件都在components文件夹中

#### 3、VueApp.vue

```
<template>
    <div>
        <img src="./assets/logo.png" alt="logo">
        <VueSchool/>
        <VueStudent/>
    </div>
</template>

<script>
import VueStudent from './components/VueStudent.vue';
import VueSchool from './components/VueSchool.vue'

export default {
    //引入组件：
    name: 'VueApp',
    
    components: {
        VueSchool:VueSchool,
        VueStudent:VueStudent
    }
};
</script>

<style lang="scss" scoped>

</style>
```

VueApp.vue 管理其它的组件

#### 3、main.js

```
// 该文件是整个项目的入口文件
import Vue from 'vue'
// 引入App组件，它是所有组件的父组件
import VueApp from './VueApp.vue'
// 关闭vue的生产提示
Vue.config.productionTip = false

new Vue({
  // el:'#app',
  //将App组件放入容器中
  render: h => h(VueApp),
}).$mount('#app')
```



#### 4、index.js

```
<!DOCTYPE html>
<html lang="">

<head>
  <meta charset="utf-8">
  
  <!-- 针对IE浏览器的一个特殊配置，含义是让IE浏览器以最高的渲染级别渲染页面 -->
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  
  <!-- 开启移动端的理想视口 -->
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  
  <!-- 引入和index.js同一级别目录下的favicon.i文件 ，使用这种格式是为了避免解析出错-->
  <link rel="icon" href="<%= BASE_URL %>favicon.ico">
  
  <!-- 配置网页标题 -->
  <title><%= htmlWebpackPlugin.options.title %></title>
</head>

<body>
  <!-- 当浏览器不支持JS时，noscript中的元素就会别渲染 -->
  <noscript>
    <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
  </noscript>
  <!-- 容器 -->
  <div id="app"></div>
  <!-- built files will be auto injected -->
</body>

</html>
```

运行：新建终端，运行npm run serve

### 二十三,render函数

