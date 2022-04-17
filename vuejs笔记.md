# Vuejs

## 渐进式概念

对于引入新框架的项目，可将一部分页面用新框架代码替换旧框架代码，循序渐进地替换并不起冲突。（新框架可兼容于旧框架使用）



## Vue的加载使用

1、CDN（分为开发环境及生产环境）开发环境适用于开发阶段调试

用语句将vuejs从服务器连接

2、下载引入

直接下载至本地通过script导入

3、NPM安装（实际项目使用）



## 响应式概念

当数据发生改变时（赋值更新），在页面直接显示更新后的状态。



## MVVM模式在vue的实现

model（数据层）：plain JavaScript object（定义对象）

view（视图）：DOM（实际可以看到的界面）

view model（DOM listener、data bindings）：	Vue（实现监听及绑定）



## Vue Options

创建VUE实例可添加的属性，如下，

el：接收css选择器字符串或element，选定作用的节点；

data：接收对象或函数（在组件模式下为函数），将对象内的变量通过引用加载到DOM内

methods：接收函数

```vue
<div id="app">
    {{massage}}
</div>
<script src="../js/vue.js"></script>//载入vue
let app = new Vue({
	el: "#app",
	data: {
		massage = "print",
		age = "20"
}，
	methods: {
		sayhi: function(){
			console.log("hi"),
}
}
})
```

### tip方法与函数的区别

直接定义的称为函数；构造函数内定义，通过实例调用的函数称为方法。



## Vue的生命周期

指vue或组件自创建开始至销毁的全过程。在生命周期中，有接口可传入函数（beforecreate、created、beforemount、mounted、beforeupdate、updated、beforedestroy、destroyed）。当定义函数后，会在不同阶段回调应用函数。



### tip前端缩进方式

缩进两个空格

## 插值操作Mustache

形如 {{message}}，将data的数据传入element，也可以传入表达式。实现响应式



## 指令

在节点中以attribute存在的以"v-"开头的代码为指令。为存在该属性的节点添加预设的功能。

### v-for

从data定义的数组逐个读取，可返回。形如：

```vue
<div id="app">
    <p v-for="(item,i) in lsit">{{item}}</p>       //a \n b \n c \n d \n e
</div>
<script>
    let app = new Vue({
        el:"#app",
        data: {
            list: ["a","b","c","d","e"]
        },
    })
</script>
//item返回列表各个项，i返回索引。
```

也可以遍历对象：

```vue
<div id="app">
    //只能获取到value，lce,22,1.65
    <p v-for="value in lsit">{{value}}</p>
	//获取value和key
    <p v-for="(value,key) in lsit">{{value}}+{{key}}</p>
	//获取value、Key、index
    <p v-for="(value,key,index) in lsit">{{value}}+{{key}}+{{index}}</p>
</div>
<script>
    let app = new Vue({
        el:"#app",
        data: {
            list: {
                name: "lce",
                age: "22",
                height: "1.64"
            }    
        },
    })
</script>
```

对数组进行操作（特别是插入操作），增加key属性，并赋值需要渲染出来的变量以提高性能。（加key必须保证数组数据唯一性）

### v-on

监听节点的事件并调用函数，如下：

```vue
<div id="app">
    <button v-on:click="btnclick"></button>//语法糖写法(@click)
</div>
<script>
    let app = new Vue({
        el:"#app",
        methods:{
            btnclick:function(){
                console.log(this.el+"clicked")
            },
        },
    })
</script>
//发生一次事件则触发mthods内的回调函数。
```

当函数需要参数时，需要在v-on属性传参。如当需要传参时，仅在调用函数变量后加（），显示undefined。

当需要传参但未在变量后加（）时，传入事件event对象。当需要参数同时需要返回event时，可传入

```vue
<div id="app" @click="btnclick(123，$event)"></div>
<script>
new Vue({
    el:'#app',
    methods: {
    //es6创建函数增强语法
	btnclick(abc,event) {
    console.log(abc,event)
},
}
})
</script>
```

#### v-on修饰符及修饰符列表

```vue
<div id="app" @click.stop="btnclick(123，$event)"></div>
```

属性语法后.stop格式为v-on修饰符，意味取消冒泡

### v-once指令

只对元素或组件渲染一次，即断开响应式。

### v-html指令

接收data里的一个html格式的字符串，以html而非字符串的形式展现。例：

```vue
<div v-html = "<a href="www.baidu.com">百度一下</a>>"></div>
//百度一下，可点击
```

### v-text

```vue
<div v-text = "massage"></div>
<div>{{massage}}</div>
```

### v-pre

显示文本内的信息而不按vue方式解析。

### v-cloak

添加给节点，当vue未解析时，存在v-cloak属性，当vue解析完成是，v-cloak属性自动删除。

可以设置该指令display：none，在vue未解析之前隐藏节点，反正mustache语法被感知。

### v-bind

设置属性响应式，当属性的变量发生改变时响应改变，属性可接收形如{active:true,line:true}对象，例：

```vue
<div v-bind:class=“divtop”></div>
//可以将对象语法设置为函数
//<div class="title" :class=getclasses()>你好！</div>
<div class="title" :class=“{active:isactive,line:isline}”>你好！</div>
<button v-on:click="btnclick"></button>
<script>
    let app = new Vue({
        el:"#app",
        data: {
       		isactive:true,
        	isline:true,
   		},
        methods: {
            btnclick: function(){
                this.isactive = !this.isactive,
            },
            //getclasses: function(){
            // return {active:this.isactive,line:this.isline},
            //},
            //设置为函数并调用 
  		},
    })
</script>
//class动态绑定（对象语法）
```

v-bind可以与属性通过对象语法与数组语法动态绑定。对象语法如{font-size,"50px"}，对于非变量需要加上双引号；也可以在methods定义return函数调用。数组语法即在data定义多个属性的对象，然后用 [ ] 一起调用。

### v-if/v-else-if/v-else

vue判断指令，形如

```vue
<p v-if="true/false"></p>
//实际开发一般处理为
		<div id="app">
		    <div v-if="ishello">
		        hello
		    </div>
		    <div v-else>
		        world
		    </div>
		    <button @click=changehello()>
		        按钮
		    </button>
		</div>
		<script>
		    new Vue({
		        el: "#app",
		        data: {
		            ishello: true
				},
		        methods: {
					changehello(){
					this.ishello = !this.ishello
					}
				},
		    })
		</script>
```

当布尔值为true时，显示对应的元素节点，当布尔值为false时，不显示对应的节点。通常用于切换显示功能。

对于切换的两个节点内含有text属性的input标签时，尽管不为同一input，但输入文本框内的字符不会消失。

原因：vue存在虚拟DOM，在进行DOM渲染时，出于性能考虑，会尽可能复用已经存在的元素，而非重新创建新的元素。同时会对DOM内容进行对比，修正当前需要渲染。

解决方法：给两个不希望复用的标签增加key属性，并给予不同的值。

### v-show

与v-if类似，当传入为true时，显示节点，传入false时，不显示节点。

#### 与v-if不同点

v-show不显示节点的逻辑是通过修改样式上的display值为none，v-if不显示节点则直接在DOM中去除。

### v-model

用法如下：

与text、radio、checkbox（单个、多个）、sele ct。

理解绑定的两个内容：元素标签上的value值及data的变量值

```vue
<div id="app">
    //文本框内显示”hello“，删除hello时，{{message}}同步会变换。
    <input type="text" v-model="message">{{massage}} 
    
    //单选框，赋值v-modle可以使得单选框互斥（没加之前赋值相同的name）
    <input type="radio" id="male" value="男" v-modle="sex">男
    <input type="radio" id="female" value="女" v-modle="sex">女
    //动态显示单选框内容
    <p>{{sex}}</p>
    
    //checkbox与v-model结合两种可能：单个勾选框和多个勾选框
    //单个勾选框
    <input type="checkbox" value="agree" v-modle="isagree">我同意
    //显示单个多选内容，对应布尔类型
    p>{{isagree}}</p>

    //多个勾选框
    <input type="checkbox" value="1" v-modle="hobbies">1
    <input type="checkbox" value="2" v-modle="hobbies">2
    <input type="checkbox" value="3" v-modle="hobbies">3
    <input type="checkbox" value="4" v-modle="hobbies">4
    //显示对个多选内容，显示数组
    p>{{hobbies}}</p>

	//select：单个与多个选择框
	//单个，自动选定默认值
    <select name="num" v-model="fruit">
        <option value="1">1</option>
    	<option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
	</select>
	
	//多个，需要添加属性multiple，一样需要与数组绑定
	<select name="num" v-model="fruits" multiple>
        <option value="1">1</option>
    	<option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
	</select>
</div>
<script>
    let app = new Vue({
        el:"#app",
        data: {
            massage: "hello"，
            sex: "男",
            isagree:"false",
            hobbies: [],
        	fruit:"2"，
        	fruirs:[]
        }
    })
</script>
```

#### 双向绑定概念

指的是通过v-modle引入的变量直接绑定到元素节点上。经绑定的内容能实现响应式。对元素节点内容进行修改时，能同步改变变量的值。以上的特性称为双向绑定。

实质：v-model的实质为用v-bind绑定value的变量与@input触发变量赋值为event.target.value的结合。

```vue
<div id="app">
    <input type="text" v-bind:value="massage" v-on:input="massage = $event.target.value">
</div>
<script>
    let app = new Vue({
        el:"#app",
        data: {
            massage: "hello"
        }
    })
</script>
```

#### 值绑定

相当于有已知变量用v-bind绑定到标签上

#### v-model修饰符

lazy修饰符：v-model.lazy="massage"。修改value时，只有在键入enter或者失去焦点才会响应。

number修饰符：v-model.number="age"。v-model在传参时默认为字符串，用number修饰符只接收数字类型。

trim修饰符：v-model.trim="name"。去除键入的字符串左右多余的空格。

## 计算属性（computed）

当需要使用经过计算后的属性时，可定义计算属性。

```vue
<div id="app">
    <p>
        {{fullname}}
    </p>
</div>
<script>
    let app = new Vue({
        el:"#app",
        data: {
       		firstname: "lee",
            lastname: "chenge",
   		},
        //computed可以当成是与methods一样的方法，接收定义函数，computed强调函数的结果，methods强调使用函数的方法，因此在methods命名时函数名前一般为动词。
		computed: {
            fullname: function(){
                return this.firstname +" "+ this.lastname,
            }
        },
        // computed完整版,set方法接收传入的参数
        computed: {
            fullname: {
                set: function(newvalue){
                    
                },
                get: function(){
                return this.firstname +" "+ this.lastname,
                }
            }
        },
        //
    })
</script>
```

computed可以当成是与methods一样的方法，接收定义函数，computed强调函数的结果，methods强调使用函数的方法，因此在methods命名时函数名前一般为动词。

computed实质为属性，如上 。

### computed与methods的区别

computed属性会进行缓存，如果多次调用，只会计算一次，效率更高。而methods每次调用都会计算一次。

##  html知识

label标签：点击文本时自动选中相应的表单控件。对应方式如下：

1、将input标签直接包含于label标签中

2、在label标签用for赋值input的id值进行关联

## 组件化概念

将页面进行拆分成一个个小的功能块，每个功能块完成属于自己的独立功能。易于管理与维护。

### Vue组件化思想

提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。

任何的应用都会被抽象成一颗组件树

### 注册组件的基本步骤

三步走：

1、创建组件构造器（调用Vue.extend（）方法）

2、注册组件（调用Vue.component（）方法）//component——组件

3、使用组件（在实例的作用范围内使用组件）

```vue
<div id="app">
    //3、使用组件
    <mycpn></mycpn>
<script>
    //1、创建组件构造器,接收对象，用``可以识别换行
    let cpnc = Vue.extend({
        template:`
        <div>
    		<h2>标题</h2>
    		<p>内容</p>
    	</div>
        `
    })
    //2、注册组件（传入两个参数，标签名和组件构造器，全局）
    Vue.component("mycpn",cpnc)
    //全局语法糖：结合1和2
    Vue.component("mycpn",{
        template:`
        <div>
    		<h2>标题</h2>
    		<p>内容</p>
    	</div>
        `
    })
    //语法糖结束，省去创建组件的步骤
    let app = new Vue({
        el:"#app",
        data: {
            massage: "hello"
        }
    })
</script>
```

### 全局、局部组件

全局组件：可以用于所有Vue实例中

局部组件：创建构造器和使用组件不变，在data中注册组件变成局部组件。如下：

```vue
//局部组件注册方式
<script>
let cpnc = Vue.extend({
        template:`
        <div>
    		<h2>标题</h2>
    		<p>内容</p>
    	</div>
        `
    })
let app = new Vue({
        el:"#app",
        data: {
            massage: "hello"
        }
    	//只能用以app绑定的id实例内
		component: {
			mycpn: cpnc 
        //标签名：组件名
    	//局部语法糖
    	component: {
			mycpn: 
    			{
        		template:`
       			<div>
    				<h2>标题</h2>
    				<p>内容</p>
    			</div>
        		`
 			   }
		}		
    })
</script>
```

### 父组件与子组件

注册在另一个组件构造器的组件构成父子关系，被注册的组件称为子组件、注册所在的组件称为父组件，如下：

```vue
<scrpit>
//1、创建一个组件构造器
	let cpnc1 = Vue.extend({
        template:`
        <div>
    		<h2>标题</h2>
    		<p>内容</p>
    	</div>
        `
		})
//2-1、在一个组件构造器中注册另一个组件
	let cpnc2 = Vue.extend({
		 template:`
        <div>
    		<h2>标题</h2>
    		<p>内容</p>
    	</div>
    	<cpn1></cpn1>
        `
		components:{
			cpn1:cpnc1
			//标签名：组件名
		}
    	})
	let app = new Vue({
        el:"#app",
        data: {
            massage: "hello"
        },
		component：{
			cpn2:cpnc2
    })
</scrpit>
```

形成父子组件后，即可以在父组件中直接调用子组件。当子组件没有被全局、局部注册过时，直接进行调用无效。 

局部组件是一种特殊的父子组件关系，其中，父组件为vue实例所在的根组件，子组件为注册在vue实例中的组价。

### 组件模板分离

第一种：用type=“text/x-template”的script标签包含需要的内容，用id进行引用

```vue
<script type="text/x-template" id="cpnc1">
	<div>
    	<h2>标题</h2>
    	<p>内容</p>
    </div> 
</script>
<script>
Vue.component("cpn1",{
	template: "#cpnc1"
})
</script>
```

第二种：用template标签

```vue
<template id="cpnc2">
	<div>
    	<h2>标题</h2>
    	<p>内容</p>
    </div>
</template>
<script>
Vue.component("cpn2",{
	template: "#cpnc2"
})
</script>
```

template标签的子节点有且只能有一个

### 组件数据

组件无法访问Vue实例数据。组件的数据存放在注册组件时component方法的data中，特别的是，data是一个函数。并且不止可以放数据，同时可以存放methods、computed于component之下，如下：

```vue
<template id="cpnc1">
	<div>
        <h2>{{title}}</h2>
        <p>{{content}}</p>
    </div>
</template>
<script>
Vue.component("cpn1",{
    template:"#cpnc1",
    data(){
        return{
            title:"标题"，
            content:"内容"
        }
    }
})
</script>
```

#### 为什么组件里data是一个函数

（以计时器组件为例）：在多次引用同个组件的时候，data作为一个函数让return返回的对象不是同一个对象，可以让数据不共用，不会相互产生印象。

若想要让数据共享，可以创建包含数据的对象，并让data return这个对象，即可共用数据。

```vue
<div id="app">
	<counter></counter>
    <counter></counter>
    <counter></counter>
</div>
<template id="temp">
	<div>
		<h2>当前计数：</h2>
		<p>{{count}}</p>
		<button @click="decrement()" :disabled="count<=0">-</button>
		<button @click="increment()">+</button>
		<button @click="count=0">复位</button>
	</div>
</template>
<script src="./js/vue.js"></script>
<script>
	Vue.component("counter",{
		template: "#temp",
		data(){
			return {
				count: 0
			}
		},
		methods: {
			increment(){
				this.count++
			},
			decrement(){
				this.count--
			}
		}
	})
</script>
<script>
	let app = new Vue({
		el:"#app"
	})
</script>
```

### 父子组件的通讯

在实际开发中，由父组件向服务器请求得到数据再传递给子组件进行展示。vue实例存在的层级为根组件，可以当成是最顶层的父组件。传递方式如下：

#### 父传子——props方法

父传子一般是将父组件的数据传至子组件，用props方法，逻辑为：1、完成子组件的注册后，父组件有数据需要传递到子组件中；2、子组件用props方法创建子组件变量接收父组件数据；3、在使用组件时通过v-bind属性的方式将props内的变量与父组件数据通讯，完成整个过程。

代码如下：

```vue
<div id="app">
//3、使用组件 
	<temp :clist='list' :cnumber='number'></temp>//完成父子组件间的通讯
</div>
//1-1、用组件模板分离的组件构造器（模板）
<template id="temp">
	<div>
        //在子组件间使用胡子语法
		<h2>{{cnumber}}</h2>
		<p>{{clist}}</p>
	</div>
</template>
<script src="./js/vue.js"></script>
<script>
//1-2、用组件模板分离的组件构造器（主体，未使用语法糖）
//使用语法糖，可以把temp作为一个对象：
//	let temp = {
//		template:'#temp',
//		props:['clist','cnumber']
//  }
	let temp = Vue.extend({
		template:'#temp',
		props:['clist','cnumber']//创建子组件可以用的变量
	})
	let app = new Vue({
		el:'#app',
		data: {
//在父组件里的数据
			list: ['1','2','3','a','b'],
			number: '112233'
		},
//2、注册组件
		components:{
			temp // temp: temp语法糖 标签名:组件名
		}
	}) 
</script>
```

props既可以传入数组，也可以传入对象。

数组包含用于子组件的变量，需在变量增加引号。

对象可以规定传给子组件变量的父组件变量的数据类型。或者该子组件变量的更多需求。（对该对象的键传入对象类型的值）

```vue
<script>
<外层为子组件>
props: ['carray','cstring','cnumber'，'cobject']
props: {
	carray: Array,
	cstring: String,
	cnumber: Number,
	cobject: {
		type: String,       //限制传入变量数据类型
		default: "112233",	//在没有接收到出入数据时的默认值
        required: 'true'    //布尔值。true时必须传入数据
	}
}
</外层为子组件>
</script>
```

当采用以上objects定义方式时，若type为array或者object，则默认值应传入一个函数，即：

```vue
	default(){
		return [](当数组时)//return {}(当对象时)
}
```

##### 父传子驼峰标识警告

v-bind不支持驼峰标识，因此创建子组件变量用驼峰命名时，在使用时无法显示。

解决方法：当子组件变量名为cMassage，绑定时应写成 : c-massage : "massage"。即每个大小写分隔处需要增加   ” - “ 。

#### 子传父——自定义事件$emit Events

子传父一般传递子组件发生的事件给父组件。通过自定义事件emit方法。emit接收两个参数，发射的事件名与发射的参数。逻辑为：

1、在子组件需要监听的标签上增加v-on监听事件，触发子组件事件回调函数。

2、回调函数设置this.emit(自定义事件事件名)，并发射事件信号

3、在使用组件时（父组件内）通过v-on属性的方式使得父组件监听自定义事件，触发父组件事件回调函数。

（自定义事件返回”item“）

当子组件的事件触发时，触发回调函数-发射自定义事件至使用组件处（父组件内），触发自定义事件的回调函数。达成事件的传递

```vue
<div id="app">
//3、自定义事件被触发
	<temp @beclicked="cpnclick"></temp>
</div>
<template id="temp">
	<div>
//1、需要传递的事件
		<button v-for="item in list"
		@click="noteclicked(item)">{{item.name}}</button>
	</div>
</template>
<script src="./js/vue.js"></script>
<script>
	let temp = Vue.extend({
		template:'#temp',
		data(){
			return{
				list:[
					{id:'a',name:'111'},
					{id:'b',name:'222'},
					{id:'c',name:'333'},
					{id:'d',name:'444'},
				]
			}
		},
		methods: {
//2、事件触发回调-发送自定义事件
			noteclicked(item){
				this.$emit('beclicked',item) //自定义事件事件名
			}
		}
	})
	let app = new Vue({
		el:'#app',
		components:{
			temp // temp: temp语法糖 标签名:组件名
		},
		methods: {
//调用回调，可以传输子组件的事件属性
			cpnclick(item){
				console.log("由于接收到子组件的事件导致父组件发生回调" ,item)
			}
		}
	}) 
</script>
```

### 组件访问

概念：子组件与父组件之间相互找到对方的数据，通过对象直接访问。

#### 父访问子

有两种访问方法：$children或者$refs(renference)

```vue
<div id='app'>
//增加refs的引用属性
    <cpn ref='abc'></cpn>
	<cpn></cpn>
	<cpn></cpn>
	<button @click="ischildren">按钮</button>
</div>
<template id='temp'>
	<div>
	    <h2>你好</h2>
        <p>世界</p>
    </div>
</template>
<script src="./js/vue.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        components: {
            'cpn':{
            template:'#temp',
            data(){
                return{
                	message:"你好"     
                }
            },
			methods: {
				inchildren(){
					console.log('children')
				}
			}
            }
        },
        methods: {
            ischildren(){
//$childrem返回包含组件的数组，使用多少个既生成多少个
				console.log(this.$children[0].message);
				this.$children[0].inchildren()
//$refs返回对象类型键值为引用属性的值及对应组件对象，访问数据时可以按对象进行访问
                console.log(this.$refs.abc.message);
				this.$refs[0].inchildren()
			}
        }
    })
</script>
```

#### 子访问父

有两种访问方法：$parents或者$root

```vue
<div id='app'>
    <cpn></cpn>
</div>
<template id='temp'>
	<div>
        <h2>你好</h2>
        <p>世界</p>
        <button @click="ischildren">按钮</button>
    </div>
</template>
<script src="./js/vue.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        data： {
        	message: '123123'
   		}
        components: {
            'cpn':{
            template:'#temp',
			methods: {
//$parent访问父组件，有vue实例或vue组件两种情况 
                ischildren(){
				console.log(this.$parent.message);
				this.$parent.inchildren1();
//$root直接访问所在的Vue实例。
        		console.log(this.$root);
            	}
			},
		},
        methods: {
            	inchildren1(){
					console.log('children1')
				},
			}
        },
    })
</script>
```

实际开发中不建议使用$parent进行访问，因为会造成耦合度低，子组件复用性不足。

## slot插槽

slot为组件提供了自定义的块，用法如下：

```vue
<div id="app">
//替换组件中slot标签中间为充当插槽的位置
    <cpn><button>按钮</button></cpn>
    <cpn></cpn>
    <cpn></cpn>
</div>
<template id='temp'>
	<div>
        <h2><标题/h2>
        <p>文本</p>
//插槽的位置为将被替换的地方
        <slot></slot>
//设置默认值，当使用组件中间没有插入时，显示默认值。
        <slot><p>默认</p></slot>
    </div>
</template>
<script>
    let app = new Vue({
        el: '#app',
        components: {
            'cpn': {
                template: '#temp'
            }
        }
    })
</script>
```

当使用组件中间有多个标签，只有一个slot时，将多个标签替换掉一个slot。同样条件下，slot标签可以预先设置默认标签，当有另外标签时默认标签失效。

当使用组件只有一个标签，且有多个slot时，增加标签到slot的数量。

### 具名插槽（新版本已更新）

可以给插槽slot一个name值，只有当使用组件上有slot=‘对应name值名’时。才发生替换。

```vue
<div id="app">
//替换组件中slot标签中间为充当插槽的位置
    <cpn></cpn>
    <cpn><button slot=‘center’>按钮</button></cpn>
    <cpn></cpn>
<template>
	<div>
        <slot></slot>
        <slot name='center'></slot>
    </div>
</template>
</div>
```

如上，只替换具有相对name名slot名的solt标签

### 编译作用域（新版本已更新）



## 前端模块化

## webpack

## Vue CLI

## Vue项目

由三部分构成：

1、<template>组件代码

2、<script>js代码

3、<style>样式代码

实际运行中vue文件会渲染成render函数进行编译，所以在实例开发中可以在组件化中使用驼峰命名法
