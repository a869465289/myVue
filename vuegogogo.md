### 1.声明变量  let和const

​        let声明的变量: 1.属于局部作用域  2.没有覆盖现象123
​        const声明的是常量,一旦声明 不可修改
​        const声明的常量属于局部作用域

### 2.模板字符串 好处

​        tab键上面的反引号
​        如果说你要拼接一串字符串,那么不需要咱们直接的+去拼接,使用反引号来拼接,拼接的变量使用${变量名}

### 3.函数的书写

    es6箭头函数的使用:
    
    function(){} ==== ()=>{}
    
    箭头函数的使用带来的问题:
        1.使用箭头函数 this的指向发生了改变
        2.使用箭头函数 arguments不能使用

### 4.对象的创建

对象的单体模式
fav(){
                
}
等价于:

function fav(){
    
}

等价于
var fav = function(){
    
}

### 5.es6中类的概念

// es6中创建对象的方式 使用class
        class Person{
            constructor(name,age){
                this.name = name;
                this.age = age;
            }
            showName(){
                alert(this.name)
            }


        };
    
        var p2 = new Person('张三',20);
        p2.showName();


----------------------------------------------------------------------------------------------------------------------------------------------------------

## vue的基本环境配置

1. 下载node.js(因为需要用到npm)
2. 利用npm对项目进行初始化：npm init
3. 下载vue的包：npm install vue --save



## vue的起步

```vue
<div id="app">
			<!-- 模板语法进行插值 {{}} 可以运算和判断 不能使用逻辑 -->
			<h3>{{msg}}</h3>
		</div>
		<!-- 1.引入vue的包 -->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			// 创建vue实例化对象
			
			let app = new Vue({
				el: '#app', // 目的地, 绑定的元素
				data: {
					// 数据属性, 数据驱动视图
					msg: 'hello Vue'
				}
			})
		</script>
```

1. 在Vue中，实例化的对象里面的属性在浏览器打开时都有$在属性前面，是为了与我们自己定义的属性进行区分。
2. 同时可以看到我们定义了一个appd的对象，app.$el 与 document.getElementById(app) 是相等的。
3. 同时实例化vue之后，vue就是一个方法，挂载在窗口上。



# vue的指令系统



## v-text and v-html  

```vue
<div id="app">
			<h3>{{msg}}</h3>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			new Vue({
				el:'#app',
				data:{
					msg:'hello 指令系统',
					msg1:'我是html',
					msg2:'<a href="#">我是text</a>',
				},
				template:`
				<div>
					<h3>{{msg}}</h3>
					<h3 v-text='msg1'></h3>
					<h3 v-html='msg2'></h3>
				</div>
				` // 优先级大于el, 存在则直接找模板,不走绑定元素
			});
		</script>		
```



- 与js中的innerHTML 和innerText 类似，v-text与{{}}类似
- text插入文本，html可插入标签



## v-if and v-show

```vue
<script type="text/javascript">
			new Vue({
				el:'#app',
				data:{
					isShow:false,
				},
				template:`
				<div>
					<h3>{{msg}}</h3>
					<div class='box' v-if='isShow'></div>
					<div class='box' v-show='isShow'></div>
					<div v-if='Math.random() > 0.5'>
						出现
					</div>
				</div>
				` 
			});
```

`			v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被*销毁和重建*。v-if` 也是惰性的。如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。相比之下，`v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。



## v-on 数据驱动视图的开始

```vue
<script type="text/javascript">
			new Vue({
				el:'#app',
				data:{
					menuList:[
						{id:1, name:'大腰子', price:60},
						{id:2, name:'宫保鸡丁', price:50},
						{id:3, name:'炸黄花鱼', price:40},
						{id:4, name:'糖醋里脊', price:30},
					],
					object:{
						name:'Tom',
						age:18,
						fav:'lol'
					}
				},
				template:`
				<div> 
					<ul>
						<li v-for = '(item, index) in menuList'>
						<h3>索引:{{index}}</h3>
						<h3>菜名:{{item.name}}</h3>
						<h3>价格:{{item.price}}</h3>
						</li>
					</ul>
					<ul>
						<li v-for = '(value, key) in object'>
							{{key}}--{{value}}
						</li>
					</ul>
				</div>
				` 
			});
		</script>		
```

​	v-on最明显的特点就是数据驱动视图，由于data里面存在的一个对象和一个数组，进行遍历之后，才展示与网页上。**需要注意的是，数组与对象的遍历方式有部分不同！**



## v-bind

<div id="app">
		</div>
```vue
	<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
		new Vue({
			el:'#app',
			data:{
				isRed:true,
				href:'https://www.baidu.com'
			},
			template:`
			<div>
				<div class='wrap' :class='{active:isRed}'></div>
				<a :href="href">百度</a>
			</div>
			` 
		});
	</script>		
```
- v-bind又称绑定，在示例代码中如果isRed为true,**则active会添加至类中**
- 在href中，就可就data里面的数据传入进去， 绑定属性之后就可以使用data的数据了。



## v-on and v-if

```vue
<div id="app">
			<button v-on:click="showHandler">按钮</button>
			<div class="wrap" v-if="isShow"></div>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			new Vue({
				el:'#app',
				data:{
					isShow:true,
				}, 
				methods:{
					showHandler(){
						this.isShow = !this.isShow;
					}
				}
			});
		</script>		
```

​	**v-on可以绑定js的所有事件，通过改变data里面的数据，实现对dom的操作**



## v-on and v-bind

```vue
<div id="app">
			<button type="button" @click='changeColor'>切换</button>
			<div class="wrap" :class="{active:isBlue}">
			</div>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			new Vue({
				el:'#app',
				data:{
					isBlue:false
				}, 
				methods:{
					changeColor(){
						this.isBlue = !this.isBlue
					}
				}
			});
		</script>		
```

​	其实也是通过添加class来实现标签颜色的切换



## 指令系统之轮播图实现

```vue
<div id="slider">
			<img :src="imgSrc" >
			<ul>
				<li v-for='(item, index) in imgArr' 
				:class="{active:index === cueerntIndex}"
				@click="clickHandler(index)"
				>
					{{index + 1}}
				</li>
			</ul>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			let imgArr = [
				{id:1, imgSrc:'./image/01.jpeg'},
				{id:2, imgSrc:'./image/02.jpeg'},
				{id:3, imgSrc:'./image/03.jpeg'},
				{id:4, imgSrc:'./image/04.jpeg'}
			]
			
			new Vue({
				el:'#slider',
				template:'',
				data(){
					return{
						imgArr:imgArr,
						cueerntIndex:0,
						imgSrc:'./image/01.jpeg'
					}
				},
				methods:{
					clickHandler(index){
						this.cueerntIndex = index;
						this.imgSrc = imgArr[index].imgSrc;
					}
				}
			})
		</script>
```

​	这里说一下实现的逻辑：

1. 首先我们定义了一个存于本地的图片数组，将数组赋给Vue对象的data
2. 通过v-for对索引进行遍历， 设置一个当前图片页的值，当图片页的值与索引相等时添加active给li标签。由于cueerntIndex是根据我们的点击事件实时变化的，所以实现点击触发索引高亮的效果。
3. 同时通过点击事件以及将img的路径通过**v-bind**绑定，在点击事件里面修改路径，实现图片的切换。
4. 最重要的就是：**数据驱动视图，由于Vue对象里面的data数据的改变，导致视图的改变。**



## V-model 双向数据绑定

```vue
<div id="app">
			<input type="text" v-model="name"/>
			<p>{{name}}</p>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			new Vue({
				el:'#app',
				data:{
					name:'alex'
				}
			})
		</script>
```

​	双向数据绑定就是data -> view, view -> data, 示例代码中input的value的改变使data发生变化，同时使p标签也发生变化，这就是双向数据绑定。**注意：双向数据绑定只允许在表单控件**

​	**实现原理**

```vue
<div id="app">
			<input type="text" :value='name' @input="changeHandler"/>
			<p>{{name}}</p>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			// Object.defineProperty() 监听属性变化
			new Vue({
				el:'#app',
				data:{
					name:'alex'
				},
				methods:{
					changeHandler(event){
						console.log(event);
						this.name = event.target.value;
					}
				}
			})
		</script>
```

​	实际是一个语法糖，需要注意的是@input="changeHandler"返回的有一个event的参数，里面携带了我们输入的值。



## 组件

![image-20191029231217341](/Users/zhouxuqiang/Library/Application Support/typora-user-images/image-20191029231217341.png)

示例代码：

```vue
<div id="app">
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			let Vheader = {
				template:`
				<div id='header'>我是头部</div>
				`
			}
			
			// 1.声明入口组件
			let Vmain = {
				template:`
					<div class='main'>
						我是入口
						<Vheader/>
					</div>
				`,
				components:{
					Vheader
				}
			}
			
			new Vue({
				el:'#app',
				// 3.使用组件
				template:`<Vmain/>`,
				data:{
					
				},
				components:{
					// 2.挂载组件
					Vmain,
				}
			})
		</script>
```

组件使用的顺序是：

1. 声明组件
2. 挂载组件
3. 使用组件

**需要注意的是，只有一个Vue对象，只有一个el:'#app'**



## props传递数据

```vue
let Vmain = {
				template:`
					<div class='main'>
						{{title}}
					</div>
				`,
				props:['title']
			}
			
			new Vue({
				el:'#app',
				// 3.使用组件
				template:`<Vmain :title='text'/>`,
				data:{
					text:'我是一个标题'
				},
				components:{
					// 2.挂载组件
					Vmain,
				},
			})
```

​	将data中的数据绑定到子组件的属性上，通过props的取到data，并进行使用。

### 示例：从爷爷组件向孙子组件传值

```vue
let Vcontent = {
				template:`
					<div class='content'>
						<ul>
							<li v-for='post in posted' :key = 'post.id'>
							<h3>我的博客标题{{post.title}}</h3>
							<h3>我的博客内容{{post.content}}</h3>
							</li>
						</ul>
					</div>
				`,
				props:['posted']
			}
			
			// 1.声明入口组件
			let Vmain = {
				template:`
					<div class='main'>
						<div class='wrap'>
							<Vcontent :posted='post'/>
						</div>
					</div>
				`,
				components:{
					Vcontent
				},
				props:['title','post']
			}
			
			new Vue({
				el:'#app',
				// 3.使用组件
				template:`<Vmain :post='posts'/>`,
				data:{
					posts:[
						{id:1, title:'组件传值', content:'通过Prop传递数据'},
						{id:2, title:'组件传值1', content:'通过Prop传递数据1'},
						{id:3, title:'组件传值2', content:'通过Prop传递数据2'},
					]
				},
				components:{
					// 2.挂载组件
					Vmain,
				},
			})
```

​	**其实传递的是属性的名字，个人理解是属性的变量名，内容就是data的值，这样理解就不会出错了。**



## 利用this.$emit，子组件向父组件传值

![image-20191030150617156](/Users/zhouxuqiang/Library/Application Support/typora-user-images/image-20191030150617156.png)



## 公共组件

​	公共组件顾名思义就是可以公共用的组件，示例代码如下：

```vue
<div id="app"></div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			
			//公共组件的创建
			//第一个为公共组件的名字, 第二个为参数
			Vue.component('Vbtn',{
				template:`<button>登录</button>`
			})
			
			let Vheader = {
				template:`<div id='head'><Vbtn/></div>`,
				// 公共组件无需挂载
			}
			
			// 局部组件的使用
			let App = {
				template:`<div>
					<Vheader></Vheader>
				</div>`,
				components:{
					Vheader,
				}
			}
			
			new Vue({
				el:'#app',
				data(){
					return{
						
					}
				},
				template:' <App/>',
				components:{
					App
				}
			})
		</script>
```

**需要注意的点**

1. 组件化之后，data必须返回一个值，用于其他组件的独立拷贝
2. 公共组件创建的格式如代码所示，使用公共组件时直接添加组件即可，不用挂载。



## Slot 分发

```vue
Vue.component('Vbtn',{
				template:`<button class='defalut' :class='type'>
					<slot></slot>
				</button>`,
				props:['type'],
			})
			
			let Vheader = {
				template:`<div id='head'>
				<Vbtn>登录</Vbtn>
				<Vbtn>注册</Vbtn>
				<Vbtn>提交</Vbtn>
				<Vbtn type='primary'>默认的按钮</Vbtn>
				</div>`,
				data(){
					return{
						
					}
				},
				// 公共组件无需挂载
			}
```

**props也可以直接传父组件的属性，无V-bind也可**



## 过滤器

```vue
<div id="app">
			<input type="text" v-model="price"/>
			<p>{{price|currentPrice}}</p>
			<h3>{{msg|reverse}}</h3>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			
			// 全局过滤器
			Vue.filter('reverse',function(value){
				return value.split('').reverse().join('');
			})
			
			new Vue({
				el:'#app',
				data(){
					return{
						price:0,
						msg:'hello vue!'
					}
				},
				filters:{ // 局部过滤器
					currentPrice:function(value){
						console.log(value);
						return '$'+value
					}
				}
			})
		</script>
```

1.  过滤器的定义与组件类似，分局部与公共
2. 局部为filters, 全局为Vue.filter

## 计算属性watch

```vue
new Vue({
				el:'#app',
				data(){
					return{
						name:''
					}
				},
				watch:{
					name:function (value) {
						if(value === 'alex'){
							alert('hahaha');
						}
					}
				}
			})
```

​	监听name的变化，但是容易导致数据滥用。



## computed计算属性

```vue
<div id="app">
			<p>{{alexDesc}}</p>
			<button @click="clickHandler">修改</button>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			new Vue({
				el:'#app',
				data(){
					return{
						myName:'alex',
						age:18
					}
				},
				methods:{
					clickHandler(){
						this.myName = 'tom';
						this.age = 20
					}
				},
				computed:{
					alexDesc:function(){
						// return this.myName + '今年' + this.age +'岁'
						return `${this.myName}今年${this.age}岁`
					}
				}
			})
		</script>
```

 通过点击事件修改data里面的值，利用计算属性去修改返回给标签的函数，实现内容的改变。

### computed的setter方法

```vue
<div id="app">
			<input type="text" v-model="alexDesc">
			<p>{{alexDesc}}</p>
		</div>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			new Vue({
				el:'#app',
				data(){
					return{
						myName:'alex',
						age:18
					}
				},
				methods:{
					clickHandler(){
						this.myName = 'tom';
						this.age = 20
					}
				},
				computed:{
					alexDesc:{
						set:function(newValue){
							console.log(newValue);
							this.myName = newValue;
						},
						get:function(){
							return this.myName;
						}
					}
				}
			})
		</script>
```

​	目前看来没有太大的用处，但是在监控数据的时候可以把表单的值在set中拿出来进行操作，可以实现部分功能。



## 生命周期钩子函数

 官网：https://cn.vuejs.org/v2/guide/instance.html#实例生命周期钩子



## $refs 获取原生DOM

```vue
			let tom = {
				template:`
				<div>哈哈哈</div>
				`,
			}
			
			let App = {
				template:`
					<div>
						<button ref='btn'>我是按钮</button>
						<tom ref ='tom' ></tom>
					</div>
				`,
				components:{
					tom
				},
				beforeCreate(){
					console.log(this.$refs.btn);
				},
				created(){
					console.log(this.$refs.btn);
				},
				beforeMount(){
					console.log(this.$refs.btn);
				},
				mounted(){
					console.log(this.$refs.btn);
					console.log(this.$refs.tom);
				}
			}
```

1. 通过refs的对象取到我们需要的DOM,但是需要在标签里面的ref绑定一个属性
2. 只有挂载数据之后才能取到标签



## $nextTick

![image-20191101155049021](/Users/zhouxuqiang/Library/Application Support/typora-user-images/image-20191101155049021.png)



后续源码补充



## **前端路由

​	首先了解一个SPA,单页面应用:**锚点值的改变后，不会立即发送请求，而是在合适的时间，发送ajax请求，局部改变页面中的数据**

### 原理

​	根据锚点值的改变去进行组件的变化

```JavaScript
<a href="#/login">登陆页面</a>
		<a href="#/register">注册页面</a>
		<div id="app">
			
		</div>
		<script src="../node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			let oDiv = document.getElementById('app');
			
			window.onhashchange = function(){
				console.log(location.hash);
				
				switch(location.hash){
					case'#/login':
						oDiv.innerHTML = '<h2>登录页面</h2>'
						break; // 必须有break,不然会穿透
					case'#/register':
						oDiv.innerHTML = '<h2>注册页面</h2>'
						break;
					default:
						break;
				}
			}
			
		</script>
```

### 基本使用

```vue
<div id="app">

		</div>
		<script src="../node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
		<script src="../node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			 Vue.use(VueRouter);
			 
			 let Login = {
				 template:`
					<h3>登录页面</h3>
				 `
			 }
			 
			 let Register = {
				 template:`
					<h3>注册页面</h3>
				 `
			 }
			 
			 let router = new VueRouter({
				 routes:[
					 {
						 path:'/login',
						 component:Login
					 },
					 {
						 path:'/register',
						 component:Register
					 }
				 ]
			 })
			 
			 let App = {
				 template:`
					<div>
						<router-link to='/login'>登录页面</router-link>
						<router-link to='/register'>注册页面</router-link>
						<router-view></router-view>
					</div>
				 `
			 }
			 new Vue({
				 el:'#app',
				 data(){
					 return{
						 
					 }
				 },
				 router,
				 components:{
					 App
				 },
				 template:`<App/>`
			 })
		</script>
```

使用vue-router的步骤

1. 引包
2. Vue.use(VueRouter)，使用vue-router，在vue对象里面注册路由，这里是router
3. 设置路由路径与加载组件
4. 在组件中使用router-link去触发路由，这里的to相当于href
5. Router-view是组件的出口，即挂载路由组件的地方



### 命名式路由

```vue
let router = new VueRouter({
				 routes:[
					 {
						 path:'/login',
						 name:'login',
						 component:Login
					 },
					 {
						 path:'/register',
						 name:'register',
						 component:Register
					 }
				 ]
			 })
			 
			 let App = {
				 template:`
					<div>
						<router-link :to="{name:'login'}">登录页面</router-link>
						<router-link :to="{name:'register'}">注册页面</router-link>
						<router-view></router-view>
					</div>
				 `
			 }
```

添加name,绑定to,进行使用。

### 路由参数params和query的使用

```vue
<script type="text/javascript">
			 Vue.use(VueRouter);
			 // route存放路由信息 router存放路由对象
			 let UserParams = {
				 template:`
					<h3>我是用户1</h3>
				 `,
				 created(){
					 console.log(this.$route.params.userId);
					 console.log(this.$router);
				 }
			 }
			 
			 let UserQuery = {
				 template:`
					<h3>我是用户2</h3>
				 `,
				 created(){
					 console.log(this.$route);
					 console.log(this.$router);
				 }
			 }
			 
			 let router = new VueRouter({
				 routes:[
					 {
						 path:'/user/:userId',
						 name:'userp',
						 component:UserParams
					 },
					 {
						 path:'/user',
						 name:'userq',
						 component:UserQuery
					 }
				 ]
			 })
			 
			 let App = {
				 template:`
					<div>
						<router-link :to="{name:'userp',params:{userId:1}}">我是用户1</router-link>
						<router-link :to="{name:'userq',query:{userId:2}}">我是用户2</router-link>
						<router-view></router-view>
					</div>
				 `
			 }
			 new Vue({
				 el:'#app',
				 data(){
					 return{
						 
					 }
				 },
				 router,
				 components:{
					 App
				 },
				 template:`<App/>`
			 })
		</script>
```

​	route存放路由信息 router存放路由对象。

​	params与query的不同之处在于url，一个是/加内容，另一个是？+键值对的形式



## 编程式导航

```vue
let App = {
				 template:`
					<div>
						<button @click ='paramsHandler'>用户1</button>
						<button @click ='queryHandler'>用户2</button>
						<router-view></router-view>
					</div>
				 `,
				 methods:{
					 paramsHandler(){
						 this.$router.push({name:'userp', params:{userId:123}})
					 },
					 queryHandler(){
						 this.$router.push({name:'userq', query:{userId:321}})
					 }
				 }
			 }
```

​	通过调用方法实现导航的功能



### 嵌套路由

```vue
let router = new VueRouter({
				//配置路由对象
				routes:[
					{
						path:'/',
						redirect:'/home'
					},
					{
						path:'/home',
						component:Home,
						children:[
							{
								path:'',
								component:Music
							},
							{
								path:'music',
								component:Music
							},
							{
								path:'movie',
								component:Movie
							}
						]
					}
				]
			})
			
```

​	通过children去嵌套，实现分发。

​	动态路由匹配是使用结构不同组件的匹配，相同的后续再看。



## 动态路由匹配

```vue
<script src="../node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script src="../node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			// 提醒一下，当使用路由参数时，例如从 /user/foo 导航到 /user/bar，原来的组件实例会被复用。
			// 因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。
			// 不过，这也意味着组件的生命周期钩子不会再被调用。
			Vue.use(VueRouter);

			let Timeline = {
				template: `
					<div>
						<router-link :to = "{name:'comDesc', params:{id:'android'}}">Android</router-link>
						<router-link :to = "{name:'comDesc', params:{id:'frontend'}}">前端</router-link>
						<router-view></router-view>
					</div>
				`
			}

			let Pins = {
				template: `
					<div>
						我是沸点
					</div>
				`
			}

			let ComDesc = {
				data(){
					return{
						msg:''
					}
				},
				template: `
					<div>
						我是{{msg}}
					</div>
				`,
				created(){
					this.msg = 'andorid';
				},
				watch:{
					'$route'(to, from){ //重点
						this.msg = to.params.id;
					}
				}

			}

			let router = new VueRouter({
				routes: [{
						path: '/timeline',
						component: Timeline,
						children: [{
							path: '',
							component: ComDesc
						}, {
							path: '/timeline/:id',
							name: 'comDesc',
							component: ComDesc
						}]
					},
					{
						path: '/pins',
						component: Pins
					}
				]
			})

			let App = {
				template: `
					<div>
						<router-link to='/timeline'>首页</router-link>
						<router-link to='/pins'>沸点</router-link>
						<router-view></router-view>
					</div>
				`
			}

			new Vue({
				el: '#app',
				components: {
					App
				},
				router,
				template: `<App/>`
			})
		</script>
```



## Keep-alive在路由中的使用

 使用缓存，可以使我们访问过的地方存在记录。
