#  Vuejs

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

## slot插槽(新版本已更新)

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

新版本已经更新为使用v-slot，语法糖为'#'。

### 具名插槽

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

### 编译作用域

对于组件及vue引用的主体，在调用数据时只会去寻找定义它们的模块上的数据。即对于同个命名的数据，当值不同时，在组件或主体调用时也不同。

### 作用域插槽

```vue
<div id='#app'>
    <cpn></cpn>
    <cpn>
        <template slot-scope='slot'>
			<span v-for='item in slot.data'>{{item}}-</span>
			<span>{{slot.data.join(' - ')}}</span>
        </template>
    </cpn>
</div>
<template id='temp'>
	<slot :data='list'>	
		<div>
			<p v-for='item in list'>{{item}}</p>
		</div>
    </slot>  
</template>
<script>
    let app = new Vue({
        el:'#app',
        component:{
            cpn:{
                template:'#temp',
                data(){
                    return{
                        list: ['1','2','3','4']
                    }
                },
            }
        },
    })
</script>
```



## 前端模块化

模块化规范——CommonJS(经过node.js实现)、AMD、CMD、ES6的modules

实际开发中，会将整个项目进行分工，并交由不同的人同时开发。在多人开发中，如果大部分代码的作用域在全局作用域的话，大概率会由于命名同一个变量导致程序出错。模块化的思想是不同人开发的部分进行封装并按接口返回，当需要调用到之前创建的变量或函数时，经过接口访问，可防止同名变量造成的混淆。

匿名函数解决方案：立即执行的匿名函数 ( function ( ) { } ) ( )，能解决同名变量的问题，但变量及函数无法复用。

```javascript
var moduleA = (function(){
    var obj = {};
    //定义number变量和sum方法
    obj.number = number;
    obj.sum = sum;
    return obj;
})()
//经过以上封装，通过moduleA可以访问到number，sum。
console.log(moduleA.number);
console.log(moduleA.sum(argument));
```

### commonJS方法

```javascript
//导出
module.exports = {
    number，
    sum
};
//导入
var {number,sum} = reqire('js文件src值')
```

### ES6模块化

1、页面如下设置

```vue
<!DOCTYPE HTML>
<html>
    <head>
        <title></title>
    </head>
    <body>
//引用js文件增加module的type属性，各个js文件相互独立。
        <script src='#1.js' type='module'></script>
        <script src='#2.js' type='module'></script>
    </body>
</html>
```

2、导出数据

```JavaScript
//js文件#1
//定义number变量，sum函数
export{
	number,
    sum
}
//直接导出方式
export num1 = '100',
//直接导出函数和类
export function sum1(num1,num2){
    return num1+num2;
}
export class Preson{
    run(){
        console.log('run!')
    }
}
//可更改命名的导出方式，整个js文件有且只有一个
let address = '广东';
export default address
```

3、导入数据

```javascript
//js文件#2
import {number,sum,sum1,Preson} form '.#1.js'
//使用number函数，sum方法,sum1函数，Preson构造函数
let sumnum =sum1('10','20');
let p = new Preson()

//更改命名的导入方式,接收export default导出内容
import add form '.#1.js'
//统一全部导出
import * as aaa from '.#1.js'
console.log(aaa.number);
```

## webpack

 webpage是一个模块打包工具。

webpack 的配置文件：webpack.config.js

### loader概念

loader在webpack作为一个转换器，将各种文件转化为js能理解的代码，以下为各种loader的配置。使用loader时需要对webpack.config,js进行配置。vue开发的常见loader有：css-loader、less-loader（css增强）、url-loader/file-loader、babel-loader（兼容性转换）、vue-loader。

部分loader还有其他依赖。

#### 配置1：

取代手动打包方式

```javascript
//命令行内输入
webpack 需要打包的文件 打包后的文件

//使用node模块
const path = require('path')
//用commonjs模块化方法定义webpack文件
module.exports = {
	entry: './src/main.js' ,//需要打包的js文件
	//打包输出的js文件，必须使用绝对地址
	//且为了提高耦合度，用动态获取方式
	output: {
	//使用node模块里的方法,将后边字符串拼接在一起，__dirname表示当前路径。
		path:path.resolve(__dirname,'dist')
		filename:'bundle.js'
	}
}
```

npm的配置文件：package.json（项目中使用webpack必须存在该文件，可用npm init或npm install express创建）

若想使用npm run xxx执行，需要在script中注册脚本名：'build':'webpack'

依赖方式：

开发式依赖（处理类似打包的一次性工作，各种loader，用npm install webpack --save-dev创建，在package.json存在于devDependencies）、
运行式依赖（在运行时也需要同步“在线”的部分，需要发布在生产版本，npm install webpack创建，在package.json存在于dependencies）

临时国内下载 npm --registry https://registry.npm.taobao.org install 包名

#### 配置2：

loader：加载webpack不可识别的非js文件

```javascript
//在主文件（入口文件通过commonjs将css文件导入）导入
requite('./css/nomal.css')
//webpack.config.js配置，在module.exports对象中加入：
module: {
	    rules: [
	      { test: /\.css$/, use:
           [
          { loader: "style-loader" },
          { loader: "css-loader" }
          ]},
	    ]
	  }
```

cssloader只负责加载，不负责解析。

styleloader负责将样式添加到DOM中。

所以在配置时，要在页面能够显示，需要添加"style-loader"，即先解析css文件，再将样式添加至DOM中，且由于use属性的读取是从从右往左的，所以"style-loader"放置与 'css-loader'之前。

**处理不为js文件依赖打包的一般方法（如css，或css加强文件less等）：**

**1、引入主文件 2、运行webpack 3、确认缺失的loader 4、install缺失的loader并在webconfig.js文件中配置loader。5、重运行webpack**

加载url-loader可以增加webpack对url图片的识别。

webpack对图片的识别：有两种方式，一种是通过url-loader（图片大小需要小于limit），一种是通过file-loader（图片大小大于limit）。通过url-loader时，需要配置webpack.config.js文件，当图片使用url-loader被识别时，需要在output内添加publicPath: 'dist/'，原因为url不会自动寻找图片所在位置，需要手动配置。

可以在option设置name（包含img、name、hash：8、ext），自定义生产的图片命名方式。

#### 配置3：

babel：基于loader，实现浏览器适配，将es6语法转为es5语法。

需要的组件——babel-loader、babel-core、babel-preset-es2015（es6，非官方推荐）

报错：es2015版本号为6.0.0，与新版本babel-loader、babel-core不兼容，webpack5与babel-loader@7不兼容

```javascript
module: {
  rules: [
    {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          //非官方推荐设置为'es2015'
          presets: ['@babel/preset-env']
        }
      }
    }
  ]
}
```

解决方法：

#### 配置4：

vue开发配置。需要安装vue并保持生产式依赖。

模块化思想，在引用vue时必须从另一个文件导出vue

```javascript
import Vue from 'vue';
const app = new Vue({
    
})
```

 版本报错：vue在构建的时候使用两个版本——runtime-only（不支持template编译）和runtime-compiler（支持template编译）。需要配置webpack文件使用对应的版本

```javascript
module.exports = {
    resolve：{
    	alias:{    //别名
    		//指定调用的文件
    		'vue$':'vue/dist/vue.esm.js'
		}
	}
}
```

### 插件plugin概念

插件作为一个扩展器，是对webpack的扩展，。通过安装后对webpack进行配置

**BannerPlugin**（webpack自带插件）

配置如下

```javascript
plugin: [
    new webpack.BannerPlugin('最终版权归xx所有 ')
]
```

**html-webpack-plugin**

打包HTML的插件，在dist文件夹（目标文件夹）生产index.html文件，将打包的js文件自动通过script插入到body

```js
//用npm下载后作一下配置
//webpack.config.js
const htmlwebpackplugin = require('html-webpack-plugin');
module.exports = {
    module:{
        plugins:[
            new htmlwebpackplugin({
                //根据模板引用
                template:'index.html'
            })
        ]
    }
}
```

**uglifyjs-webpack-plugin**

丑化生成的js文件代码，去除注释空格，对其进行压缩，配置如下：

```js
//npm下载安装uglifyjs-webpack-plugin
//webpack.config.js配置
const Uglifyjswebpackplugin = require('uglifyjs-webpack-plugin')
module.export = {
    module: {
        plugin: [
            new Uglifyjswebpackplugin()
        ]
    }
}
```

### webpack-dev-server

基于node.js，内部为express框架搭建本地服务器。作用于某一个文件，监控代码发生改变。当改变时，在内存响应改变，不会保存至本地。（版本与webpack对应，与vue-cli对应）

```javascript
//npm安装webpack-dev-server
//webpack.config.js配置

module.export = {
    devserver: {
        //作用于的文件夹
        contentBase:
        //布尔值，是否实时监听
        inline：
    }
}
//package.json配置
"script":{
    //设置open自动打开浏览器
    "dev":"webpack-dev-server -open"
}
```

### 多环境配置分离

在实际开发中，package.json包含运行所需要的库与组件，开发阶段需要增加或移除相关组件，而生成生产环境运行下的代码则需要某些组件（例如丑化插件）生成。因此，需要将开发与生产配置不同的package.json，并进行分离。

分离操作：

1、建立不同的xxx.config.js文件，可分为base.config.js（公共配置）、prod.config.js（生产配置，包含各种生产依赖）、dev.config.js（开发配置，包含webpack-dev-server等）

2、npm install webpack-merge --save-dev（配置文件合并）

3、配置xxx.config.js文件

```js
//prod.config.js配置文件
const webpackMerge = require('webpack-merge')
const baseConfig = require('./base.config')
//将需要合并的两个config.js文件按以下方式导入
module.exports = webpackMerge(baseConfig,{
    //添加生产环境的相关配置
})
```

4、在package.json指定webpack打包使用的配置文件

```js
"script": {
	//为webpack指定使用的配置文件
	"build": "webpack --config ./build/prod.config.js"
    "dev": "webpack-dev-server --opne --config ./build/dev.config.js"
}
```



## Vue实际开发

### el与template的关系

在运行的vue实例中，template所包括的内容将el所指向的节点进行替换。

```vue
<div id='app'></div>

import Vue from 'vue';
const app = new Vue({
    el:'#app',
	//template对el内容进行替换，同时可以获取vue实例内的数据及方法
	template:`
		<div>
            <h2>{{message}}</h2>
            <button @click='btnclick'>按钮</button>
		</div>
	`,
	data:{
		message:'hello'
	}，
	methods:{
		btnclick(){
			console.log('click!')
		}
	}
})
```

### Vue的终极方案

结合模块化、组件化的最终方案。

对于以上代码，可作以下变形：

```vue
<div id='app'></div>
//创建组件，对template属性进行剥离
const App = {
	//原来代码
	template:`
		<div>
            <h2>{{message}}</h2>
            <button @click='btnclick'>按钮</button>
		</div>
	`,
	//数据及方法
	data(){
		return{
			message:'hello'
		}
	},
	methods:{
		btnclick(){
			console.log('click!')
		}
	}
};
//原vue实例
const app = new Vue({
	el：'#app',
	template:`<App></App>`, //或者为单标签形式<app/>
	components:{
		App
	}
})
```

模块化App内的代码，如下：

```JavaScript
//js1文件，主文件
import App from 'js2文件地址';
const app = new Vue({
	el：'#app',
	template:`<App></App>`, //或者为单标签形式<app/>
	components:{
		App
	}
})
```

```vue
//js2文件，模块化的App
export default{
	template:`
		<div>
            <h2>{{message}}</h2>
            <button @click='btnclick'>按钮</button>
		</div>
	`,
	//数据及方法
	data(){
		return{
			message:'hello'
		}
	},
	methods:{
		btnclick(){
			console.log('click!')
		}
	}
}
```

用模板分离的思想代入vue文件。

```javascript
//可以导入全新的vue文件
import App from 'vues2文件地址';
```

```vue
//被导入的vue2文件
<template>
	<div>
        <h2 class='title'>{{message}}</h2>
        <button @click='btnclick'>按钮</button>
	</div>	
</template>
<script>
    export default{
        name: 'App',
		data(){
			return{
				message:'hello'
			}
		},
		methods:{
			btnclick(){
				console.log('click!')
			}
		}        
</script>
//甚至可以增加样式
<style scoped>
    .title{
        color:red
    }
</style>
```

单文件组件（SFC）需要依赖loader进行编译，运行如下代码

npm install vue-loader vue-template-compiler --save-dev

（vue3中vue-template-compiler被新的文件替换）

webpack.config.js配置

```webpack
{
	test:/\.vue$/,
	use: {
		[
			{loader:'vue-loader'}
		]	
	}
}
```

运行报错：缺失插件（vue-loader14.0.0版本以上需要额外安装插件plugin），解决方法：更换vue-loader版本。

## Vue CLI

脚手架工具。推荐版本vue-cli3，安装方式如下：

npm install @vue/cli -g

vue-cli3想使用2的模板可通过 npm install @vue/cli-init -g 拉取

### vue-cli2

创建项目——vue init webpack xxx（项目名）

ESLint（按es语法规范化代码）可导入自定义规范

unit test（单元测试 ）

e2e（端到端测试）

创建文件夹说明：

babelrc——设置babel转换env的具体内容（如针对某一范围等）

editorconfig——代码规范

eslintignore——es规范限制忽略范围

gitignore——上川到git忽略范围

package-lock.json——记录node-modules安装的真实版本

### vue-cli3

创建项目——vue create xxx（项目名）

## Vue-router

实现前端渲染（前端渲染是在前后端分离的基础上实现的，其原理为更改location的值而启用某些组件。）

### 安装步骤

1.1、安装vue-router（npm install vue-router --save 生产式依赖）

2.1、组件导入路由对象，并调用Vue.use(VueRouder)

2.2、创建路由实例，并传入路由映射配置

2.3、在vue实例中挂载创建的路由实例

### 项目步骤

1、创建router文件夹（可通过vue-cli自动创建）

2、创建index.js文件，配置router

```js
//index.js配置
import Vuerouter from 'vue-router'
import Vue from 'vue'
Vue.use(vuerputer)//通过Vue.use(插件)，安装插件
const router = new Vuerouter({ //创建vuerouter对象
    routes,   //将routes从router分离，用es6语法糖
    mode:'history', //将更改url中hash切换为更改history模式
	linkActiveclass:'active', //设置激活时的默认class属性名
})
const routes =[   //配置路由映射
    
]
export default router //导出router，在外部使用
```

### 使用步骤

```js
//配置routes,有多个对象构成的数组
import Home from '../component/home' //从对应目录导入组件
import About from '../component/about'
const routes = [
    {	//配置默认显示的页面，当缺省时，重定向至/home
    	path:''			
       	rediret:'/home' 
    },
    {
        path:'/home'，	//表示当url的path部分变化为当前时，则切换组件 
        component:Home，
    }，
    {
    	path:'/about'，
        component:About，
    }
]
```

```vue
<templat>
    <router-link to="/home">首页</router-link> //通过router-link实现切换url的效果
    <router-link to='/about'>关于</router-link>//通过router-view实现渲染组件的效果	
    <router-view></router-view>
</templat>
```

router实现的另一种方法：
用 v-on:click 绑定 methods，在methods方法内对url（即$router）l进行push或replace操作。

调用router时每个组件中包含$router对象，调用this.$router.push('/home')或this.$replace('/home')

### router-link属性

to：点击切换url的hash或者history

tag：改变浏览器渲染的方式（默认渲染为<a>）

replace：启用替换历史记录而非入栈的模式，无法回退页面

active-class：当点击激活某个组件时，会在被点击的标签上增加class属性（可通过赋值修改）

### 动态路由

```js
import User from '../component/home' 
const routes = [
    {	//按如下进行配置
    	path:'/user/:userId'，
        component:User，
    }
]
```

```vue
//compoment vue文件
<templat>
  <div>
    //动态路由的跳转需要严格按照配置输出，不然不显示
    <router-link to="/user/zhangsan">用户</router-link> 
    //从数据中动态获取写法
    <router-link :to="'/user/'+userId">用户</router-link>
    <router-view></router-view>
    <h2>{{userId()}}</h2>        
  </div>
</templat>
<script>
    //在组件中通过以下设置，已经获取页面数据信息,同时也是路由传递数据的一种方法
    export default{
        name:'uesr',
        compute:{
            userId(){
                //用$route获取主vue文件的数据
                return this.$route.params.userId
            }
        }
    }
</script>
```

```vue
//主vue文件
<script>
    export default {
        data(){
            useId:'lisi'
        }
    }
</script>
```

实际开发中对应的url从数据中获取，可用v-bind将数据给到属性。需要取得动态路由的信息时，可以用route（处于活跃的路由）来寻找

### router懒加载

懒加载概念：当页面的脚本全部存在在一个文件中时，由于代码量过大，用户在打开页面时会因为加载脚本导致短暂空白，影响用户体验。懒加载的作用是将各个组件使用的脚本生产单独的文件，当使用脚本时，才调用对应脚本。

设置方式：

```js
//设置方式为通过函数导入组件vue，取代 import Home from '../component/Home' 直接导入方式
const Home = ()=>import('../component/Home')
const routes = [
	{
    	path:'/home',
        component:Home
    }, 
]
```

### 嵌套路由实现

嵌套路由指在原先路由内部再配置一个路由，设置如下：

```js
//设置方式为通过函数导入组件vue，取代 import Home from '../component/Home' 直接导入方式	
const Home = ()=>import('../component/Home')
const HomeSetting = ()=>import('../component/home/HomeSetting')
const routes = [
	{
    	path:'/home',
        component:Home,
        //子路由直接在父路由中定义
        children：[
        	{
        	//子路由器不需要 /
        	path：'homesetting'，
        	componenet:HomeSetting
    		}，
		]
    }, 
]
```

```VUE
//在父组件中使用
<template>
	<router-link to:'/home/homesetting'></router-link>
	<router-view></router-view>
</template>
```

### 路由数据传递

路由间数据传递有两种方法：1、动态路由（params）2、query

query数据获取

```js
const Profile = ()=>import '../component/profile/Profile'
const routes = [
    {
        path:'/profile',
		component:Profile
    }
]
```

```vue
//主vue文件
//如想要传递数据，需要将to属性设置如下
<tenplate>
    <router-link :to='{path:'/profile',query:{name:why,age:22,height:168}}'>档案</router-link>
    //显示组件定义的内容
    <router-view></router-view>
</tenplate>
```

```vue
//componet vue文件
<template>
	<h2>标题</h2>
	//取得query数据
	<p>{{$route.query}}</p>
</template>
```

query获取数据的第二种方式（以router实现的第二种方式对应）

```vue
//主vue文件
<template>
	<button @click='profileclick'>
        档案
    </button>
</template>
<script>
    export default{
        name;'profile',
        data(){
            return{
                
            }
        },
        methods:{
            profileclick(){
                //在push的时候同步将数据传入
                this.$router.push(
                    {path:'/profile',
                     query:{
                         name:why,
                         age:22,
                         height:168}
                    })
            }
        }
    }
</script>
```

### 导航守卫

监听切换路由的事件。

可以通过生命周期进行监听。vue的生命周期：

created（）：组件被创建的时候进行调用

mounted（）：组件搭载到dom里边进行调用

updated（）：界面发生更新时进行调用（刷新或者{{}}数据发生改变）

router内置了beforeEach方法，接收一个有to、from、next参数的函数（next为函数，且必须存在）

```js
const router=[
    {
        path:'/home',
        component:()=>import '../component/Home',
        //meta对象为元数据
        meta:{
        	title:'首页'
    }
    },
]
//形如，通过前置回调实现页面的标题随激活的route切换而切换：
router.beforeEach((to,from,next)=>{
    //从from跳转到to时执行以下代码
    //meta是定义在配置路由中的设置
    document.title = to.meta.title,
    //document.title = to.matched[0].meta.title
    //解决第一页不显示的写法
    next()
})，
//后置回调不需要调用next()函数
router.afterEach((to,from)=>{
    
})
```

以上为全局守卫，关于导航守卫还包括路由共享守卫及组件内的守卫。

### keep-alive

keepalive实现路由切换组件时保存路由的状态。每次切换路由（url改变导致router-view改变）都意味着组件经历一个完成的生命周期（被create和destroy），保存路由的状态则是打断其不要destroyed（只created不destroyed）。

使用方法：

在<router-view>标签外嵌套<keep-alive>可以保持组件不被销毁，同时也带出两个回调函数activated（）和deactivated（），代表使用回调函数的组件是否处于活跃状态。只有当keep-alive嵌套时，在组件中能使用回调，否则无效。

keep-alive属性：include、exclude。两个属性接收字符串或正则表达式，include表示匹配的组件进行缓存，exclude表示匹配的组件不缓存。接收组件的name的值时，表示对应组件执行include或exclude。

## promise（期约）

promise提供了一种异步执行函数的封装方式，将多次回调的函数简洁结构。

使用方法：

new Promise（）接收一个带有resolve，reject两个参数（resolve、reject为函数）的函数。将调用异步的函数与执行的函数进行分离。

```js
//非promise形式
setTimeout(()=>{
    console.log('无期约')
},1000)

//promise形式
new Promise((resolve,reject)=>{
    //先假设延时后会执行一段代码
    setTimeout(()=>{
    	resolve();
        reject()
	},1000)
}).then(()=>{
    //在执行假设
    console.log('期约')
    //处理reject
}).catch(()=>{
    console.log('请求失败')
})
//.then(满足时调用函数).catch(不满足时调用函数)可改写为.then(满足时调用函数，不满足时调用函数)

//期约的参数
new Promise((resolve,reject)=>{
    setTimeout((data)=>{
        //传出data
    	resolve(data)
	},1000)
}).then((data)=>{
    //接收data
    console.log(data)
})
```

promise.all（）接收可遍历的对象（如数组）。一般传入promise对象的数组，仅当所有的resolve被执行时，才执行then（）方法的代码。

## Vuex

Vuex是为vue.js应用程序开发的状态管理模式。采用集中式存储管理应用的所有组件的转态，并以相应的规则保证状态以一种可预测的方式发生改变。

与自己封装的对象做对比：实现响应式。

需要通过vuex进行共享的数据：用户的登录状态，用户名称、头像、地理位置；商品的收藏，购物车的物品等。

### 单页面状态管理

state（变量）vue或者template中的属性

actions（用户行为）在页面触发的事件

view（页面）页面展示的内容

state——》view——》actions——》state

### 多页面状态管理使用

1、src创建store文件夹，创建vuex配置脚本index.js

2、在vuex配置脚本导入vue、vuex，创建并导出store实例

（包含state、mutation、actions、getters、modules对象）

state：保存状态（数据）

#### actions

：处理异步操作

```js
actions:{
  aupdateinfo(context){ //变量相当于store实例对象
  settimeout(()=>{
    context.commit('在mutations定义的方法')
    }，1000)
  }
}
```

在页面中的methods通过$store.dispatch('actions定义的方法')
经过两层调用，实质为事件触发actions异步操作，待异步操作响应时触发同步操作。

tip：可以将actions的异步操作包装成一个promise，如下：

```js
actions:{
  aupdateinfo(context){ //变量相当于store实例对象
    return new promise((resolve,reject)=>{
      settimeout(()=>{
        context.commit('在mutations定义的方法'),
        resolve()
	  }，1000)
    })
  }
}
//在触发actions的事件所在js调用then
methods:{
    updateinfo(){
      this
      .$store
      .dispatch('aupdateinfo')
      .then(res=>{
        console.log(res)
      })
    }
  }
}
```

#### mutations

：处理同步操作。在vuex脚本中配置好方法后。在监听操作的组件中添加methods方法并绑定，通过this.$store.commit('在vuex配置的方法')进行关联。（Vue.store状态更新的唯一方式）

```js
const store = new Vuxe.Store({
  state:{
      counter: 100,
      student:[
          {id:1,name:'lce',age:'18'},
          {id:2,name:'lcj',age:'15'},
          {id:3,name:'lyy',age:'20'}
      ]
  },
  mutations: {
    incrementcount(state,count){ //mutations可可以接收传入的数据
      state.counter += count 
    },
    //使用payload的写法
    incrementcount(state,payload){
      state.counter += payload.count
    }
}
}
//vue中的调用
//<button @clcik='addcounter(5)'>+5</button>                             
//组件js中的定义
export default {
  name:'app',
  methods: {
    addcounter(count){ //传入的参数称为payload，需要传递多个数值时，可以将payload当做一个对象(使用特	  殊提交)
      //1、普通提交风格（直接提交count）
      this.$store.commit('incrementcount',count) //传出数据格式的写法
      //2、特殊提交（用mutations事件类型提交）
      this.$store.commit({
          type: 'incrementcount',
          count //这里的count实质上是一个包含原count数据的payload对象
      })
    },
  }                           
}
```

#### getters

：类似于组件computed属性，写法如下：

```js
const store = new Vuxe.Store({
  state:{
      counter: 100,
      student:[
          {id:1,name:'lce',age:'18'},
          {id:2,name:'lcj',age:'15'},
          {id:3,name:'lyy',age:'20'}
      ]
  },
  getters:{
      powcounter(state){
      	return state.counter*state.counter,
      },
      more16stu(state):{ //getters可以做运算及筛选操作
        return state.stuedent.filter(s=> s.age>16)
      },
      more16stuLength(state, getters):{ //可以传入getters，在计算属性的基础上再做计算
        return getters.more16stu.length                     
      },
      moreagestu(state): { //涉及需要传入数据才能判断的可以用回传一个function
        return function(age) {
            return state.students.filter(s => s.age > age)
        }
      }
  }
})
//在vue中使用getters属性
// <h2>{{$store.getters.powercounter}}</h2>
```

#### module

相当于创建一个对象将state、getters、mutations、actions包含，可同以上方法进行使用。调用方法如下：

```js
modules：{
    a:{
        state:{
          name:'lce',  
        },
        getters:{
          fullname(state，getters，rootstate){ //getters可以通过rootstate取得外层state的数据
              return state.name+'1111'
          }
        },
        mutations:{
          nameinfo(state){
              console.log(state.name)
          }
        }    
        actions:{
          anameinfo(context){  //此刻的context不指store，而是指向模块a
              context.commit('nameinfo')
          }
        }
    },
}
//调用方法
this.$store.state.a.name //modules将state加载到对应属性上，通过store的属性及模块名直接调用
$store.getters.fullname//getters可以按之前方法直接调用
```

3、通过this.$store.state.变量名展示在view中。

### state单一状态树

 在开发中用一个store管理所有的状态，而非创建多个store对象。

### State的响应式

State响应式在对象中只对有初始化的变量进行响应(在state中已经添加)，修改参数时可以随变量改变在页面展示。
但对于直接添加进去的新的变量，则不能保持响应式，因为没有进行过变量初始化。需要用能够触发响应式的方法(如vue.set、vue.delete)进行插值或删除

### mutation类型常量

对于实际开发中，由于mutation内的方法定义过多，可以将函数名提取出来，用type进行代替。(为了防止代码编写时错误)
方法如下：
1，建立储存常量的js文件。用类型名导出函数名。
2，导入类型常量文件及对应类型，在store配置js中，导入对应类型名，mutations用以下方法编写

```js
[类型名]{
函数内容
}
```

3，导入类型常量文件及对应类型，在使用方法的js的methods中定义：

```js
方法名(payload或其他变量){
this.$ store.commit(类型名)//可使用对象模式
}
```

### store文件夹目录

state分离放在原文件夹

mutations、getters、actions创建新的脚本文件储存，通过模块化导出导入

modules内容创建文件夹并创建新的脚本文件

## axios

网络请求框架，发送请求后，返回服务器存储在对应位置的参数。

使用方法：

1、npm安装，在js文件中加载。

2、直接使用方法

```js
axios({
    url:'*' //请求的地址
    params:{ //针对get请求，可以将require内容按对象的形式传入
      type:'pop',
      page: 1 
    }
    method：'get' //请求的方法
}).then(res=>{
  console.log(res);
}) //使用promis方法
```

tip：axios包含了promis方法，可以按promis的方式进行处理

axios.all ()方法，同promise类型类型，接收多个axios实例，仅当所有请求响应时才返回结果。可用axios.spread((res1,res2)=>{

})将返回的数组结果进行拆分

全局配置

axios.defaul对象包含了请求的配置，可以进行baseurl、header等参数进行配置。（get需要配置params，post需要配置require body）

axios实例及模块化封装

axios.creat()方法创建axios实例，创建时传入配置方法中一样的属性。

使用第三方框架，需要将框架与实际调用的代码通过中间封装好的模块进行关联，防止框架替换时增加工作量。创建方法：

1、创建包含脚本文件的文件夹

2、按axios.creat()实例创建，直接return。（由于实例包含promise方法，因此在使用实例时可以直接用then，catch方法），导出模块化接口

```js
export function request(config) {
    const instance = axios.creat({
        baseurl: '*',
        timeout: 5000
    })
    return instance(config)
}
//在组件使用时
import {request} from '存放axios配置脚本文件'
export default {
    name:'home',
    methods:{
        created(){
          request({
              url:'#'
          }).then{
              res=>	{
                console.log(res)  
              }
          }.catch{
              err=>{
                console.log(err)
              }
          }
        }
    }
}
```

拦截器

可以对请求和响应进行拦截，可用于全局或者实例，语法如下：

```js
axios.interceptors.request.use(config=>{
//操作拦截内容
  return config //拦截后需要重新return出来
},err=>{

})

axios.interceptors.response,use(res=>{
//操作拦截
    return res.date
},err=>{
    
})
```

请求拦截器用于1、将数据转化为服务器能够接收的信息，2、加载时进行图标的显示

响应拦截

## Vue项目

由三部分构成：

1、<template>组件代码

2、<script>js代码

3、<style>样式代码

实际运行中vue文件会渲染成render函数（render函数可以）进行编译，所以在实例开发中可以在组件化中使用驼峰命名法

vue.config.js配置文件会读取并写入vue的设置中

### 项目构建顺序：

1、项目结构创建

2、基本css文件引入

