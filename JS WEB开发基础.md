一、BOM

### 1、window对象

#### (1)全局作用域

var 声明的定义于全局作用域的变量与函数，可作为window的属性与方法进行调用。let、const 声明的变量与函数不会添加至window对象。

#### (2)窗口关系 

top——最上层窗口：_top

parent——当前窗口父窗口：_parent

self——指向window本身：_self

#### (3)窗口位置及像素比

##### 1)位置

返回离屏幕边缘的距离screenLeft、screenTop = num css像素

移动窗口方法

moveTo（x，y）移动至绝对坐标

moveBy（△x，△y）相对移动位置，向右向下为正

##### 2)像素比

window.devicePixelRatio = 物理像素（实际）/ 逻辑像素（css）

#### (4)窗口大小

返回页面的大小（不包括浏览器边框及工具栏）innerWidth、innerHeight

返回浏览器窗口大小outerWidth、outerHeight

返回页面视口的高度宽度

document.documentElement.clientHeight、document.documentElement.clientWidth

返回布局视口的高度宽度

document.body.clientHeight、document.body.clientWidth

缩放窗口方法

resizeTo（x，y）缩放至给定大小

resizeBy（△x，△y）缩放至（x＋△x，y+△y）大小

#### (5)视口位置

文档相对于视口滚动距离的属性：

window.pageXoffset / window.scrollX

window.pageYoffset / window.scrollY

滚动页面的方法

scroll（）/ scrollTo（）

scrollBy（）

方法可添加behavior控制平滑滚动

#### (6)打开新窗口

window.open（**要加载的URL**、**目标窗口**、特性字符串、

布尔值（新窗口在浏览器历史记录是否替代当前加载页面））

特性字符串表（形如：“ 设置 = 值 ”）

| 设置       | 值     | 说明                           |
| ---------- | ------ | ------------------------------ |
| fullscreen | yes/no | 屏幕最大化，仅IE支持           |
| height     | number | 窗口高度，不小于 100           |
| left       | number | 窗口x坐标，不为负值            |
| location   | yes/no | 显示地址栏，no代表隐藏或禁用   |
| menubar    | yes/no | 显示菜单栏，默认为no           |
| resizeable | yes/no | 是否可变大小，默认为no         |
| scrollbars | yes/no | 是否在内容过长时滚动，默认为no |
| status     | yes/no | 显示状态栏                     |
| toolbar    | yes/no | 显示工具栏                     |
| top        | number | 窗口y坐标，不为负值            |
| width      | number | 窗口宽度，不小于100            |

通过创建新窗口，可对其进行类window对象的方法操作。

关闭窗口：window.close（）;（二次调用反馈布尔值是否关闭）

指向创建窗口的窗口：window.opener，可赋值null表示新窗口运行在独立的进程中

#### (7)定时器

设置一段时间后运行指定代码：setTimeout（目标代码（function包装），时间（单位：ms））；

设置每隔一段时间运行代码：setInterval（同上）——工程中尽量不使用，用setTimeout套用循环替换。

定时器返回一个超时ID（timeoutID），作为排期执行代码的唯一标识

在定时器运行期间取消超时clearTimeout（timeoutID）

#### (8)系统对话框

同步模态对话框，显示时，代码停止运行。

alert（）仅警示信息，无返回操作。

confirm（）有“ok”和“cancel”两个选项，返回“true”或“false”。

prompt（显示字符串，默认值）类似于<input tyep="text" value="默认值"/>，有“ok”和“cancel”，返回输入的值或“null”。

find（）：显示页面内搜索框；

print（）：显示打印框；

### 2、location对象

加载URL为http://foouser:barpassword@www.wrox.com:80/WileyCDA/?q=javascript#contents

| 属性              | 值                                                           | 说明                                          |
| ----------------- | ------------------------------------------------------------ | --------------------------------------------- |
| location.protocol | "http:"                                                      | 页面使用的协议。通常是"http:"或”https:“       |
| location.username | "foouser"                                                    | 域名前指定的用户名                            |
| location.password | "barpassword"                                                | 域名前指定的密码                              |
| location.hostname | "www.wrox.com"                                               | 服务器名                                      |
| location.port     | "80"                                                         | 请求的端口，若没有返回空字符                  |
| location.host     | “www.wrox.com:80"                                            | 服务器名及端口名                              |
| location.pathname | "/WileyCDA/"                                                 | URL中的路径及文件名                           |
| location.search   | "?q=javascript"                                              | **URL的查询字符串，以?开头**                  |
| location.hash     | "#contents"                                                  | URL散列值，以#开头。若没有返回空字符          |
| location.origin   | "http://www.wrox.com"                                        | URL的源地址。只读                             |
| location.href     | "http://foouser:barpassword@www.wrox.com:80/WileyCDA/?q=javascript#contents" | 当前窗口完成URL，类似于location的tostring（） |

#### (1)查询字符串操作

URLSearchParams提供get（）、set（）、delete（）方法，可检查和修改查询字符串。一般可迭代

例：

```javascript
let qs = "?q=javascript&num=10";
let searchParams =new URLSearchParams(qs);
searchParams.has("num");//"true"
searchParams.get("num");//"10"
searchParams.set("page","3")
console.log(searchParams.toString());//"q=javascript&num=10&page=3"
searchParams.delete("q")
console.log(searchParams.toString());//"num=10&page=3"
```

#### (2)操作地址

利用location.assign（）可更换location地址，导航向新的URL。给location.href或window.locaton设置一个URL，最后还是以location.assign方法调用。

修改浏览器常用location.href。

通过修改URL属性可修改URL，除hash外，修改location中任一属性都会重新加载URL。加载的URL保存在历史记录中，同时可被后退或前进（如果有的话）。

用location.replace（“URL”）操作地址，重加载后不会添加到历史记录，也不可被后退。

用location.reload（）可重新加载页面，传入参数"true"时，强制从服务器重新加载。

### 3、navigator对象

#### (1)检测插件

navigator.plugins返回浏览器安装的插件的数组，每一项包括name（插件名称）、description（插件描述）、filename（插件文件名）、length（当前插件处理的MIME类型数量）。

pligins数组的每个插件对象有一个MimeType对象，可通过中括号访问。对象有description（描述MIME类型）、enabledPlugins（指向插件对象的指针）、suffixes（MIME类型对应扩展名的逗号分隔的字符串）、type（完整的MIME类型字符串）

IE11后支持plugins及MimeTypes属性，以上定义的函数适用于所有较新版本的浏览器。通过访问navigator.plugins.name可检测浏览器是否安装对应插件。
对于低于IE11版本的浏览器，要使用专有的ActiveXObject，还需要知道插件的COM标识符。（在IE11版本，ActiveXObject在DOM被隐身，无法使用。）

两种检测方法不一致。综合检测插件方法如下：

```javascript
//适用于IE11及更新版本检测插件,此处name为插件名称
let hasplugin = function(name){
	name = name.toLowerCase();
    for(let plugin of window.navigator.plugins){
        if(plugin.name.toLowerCase().indexOf(name) > -1){
            return true;
        }
        else{
            return false;
        }
    }
}
//适用于IE10及更老版本检测插件，用此处name为插件COM标识符（IE插件检测方法）
function hasIEplugin(name){
    try{
        new ActiveXObject(name)；
        return true;
    }
    catch(ex){
        return false;
    }
}
//实际开发针对一种特定插件写一个函数
function hasFlash(){
    var result = hasplugins("Flash");
    if(!result){
        result = hasIEplugin("ShockwaveFlash.ShockwaveFlash");
	}
    return result;
}
```

plugins.refresh(" "/"true")方法用于刷新plugin属性以反映新安装的插件。接受“true”时，会重新加载包含插件的页面。否则只更新plugin而不加载网页。

#### (2)注册处理程序

navigator.registerProtocolHandler（）方法可以把网页注册处理为某种特定类型信息应用程序，将Web应用程序注册为像桌面软件一样的默认应用程序。

方法接收“要处理的协议（mailto或ftp）”、“处理该协议的URL”、应用名称。

```
navigator.registerProtocolHandler(
	"mailto",
	"http://www.somemailclient.com?cmd=&s",
	"Some Mail Client"
)
```

### 4、screen对象

screen属性如下：

| 属性        | 说明                                       |
| ----------- | ------------------------------------------ |
| availHeight | 屏幕像素高度减去系统组件高度（只读）       |
| availLeft   | 没有被系统组件占用的屏幕最左侧像素（只读） |
| availTop    | 没有被系统组件占用的屏幕最顶端像素（只读） |
| availWidth  | 屏幕像素宽度减去系统组件高度（只读）       |
| colorDepth  | 表示屏幕色彩位数（只读）                   |
| height      | 屏幕像素高度                               |
| left        | 当前屏幕左侧的像素距离                     |
| pixelDepth  | 屏幕的位深（只读）                         |
| top         | 当前屏幕端侧的像素距离                     |
| width       | 屏幕像素宽度                               |
| orientation | 返回Screen Orientation API中屏幕的朝向     |

### 5、history对象

history记录当前窗口自首次使用以来用户的历史导航记录，每个window都有自己的history。

#### (1)导航

history.go()方法：

传入数值，指前进（正值）或后退（负值）几个历史页面，0代表刷新。

传入字符串，导航到历史中含有改字符串的第一位置，可进可退。（用于旧版本浏览器）

go方法变形——back（）、forword（）。

history内含length属性，代表历史记录有多少条目。导航的第一个页面：history.length 等于1。

条目增加的标志为URL改变，无论是否刷新界面。（更改hash散列值不刷新页面同样增加历史记录）

#### (2)历史状态管理

haschange事件在URL hash值改变时触发，可以设置此时执行某些操作。

history.pushState（）方法接受三个参数，state对象、新状态的标题、相对的URL（可选）。在历史记录中增加一个记录，且此页面改变为新的相对URL，但浏览器不会向服务器发送请求。

pushState方法创建新的历史记录。当此页面为首次记录时，相当于激活了“后退”按钮。若单击“后退”，则触发了popstate事件。popstate事件对象有一个state属性，为pushState传入的state对象。初次加载的页面其state属性为null。

history.replaceState（）方法接收pushState方法的前两个参数，更新覆盖当前记录的状态，不会在添加到历史记录中。

无论是增加或者替换URL时，都应该保证服务器有对应的真实URL，否则在刷新时会使得页面报错。

## 二、客户端检测

浏览器的不同接口或不同长处短处是客户端检测存在的原因，在页面设计应先考虑程序的最大兼容性，再使用客户端检测方法克服缺陷。

### 1、能力检测

能力检测指通过传入方法，直接判断浏览器是否支持的一种简单逻辑。不需要事先知道浏览器的特性，直接检测是否存在。如：

```javascript
if(object.propertyInQuestion){
	//检测存在时,使用object.propertyInQuestion
}
```

 对于同个功能的不同方法的检测，先检测更加普遍的，在检测特殊的。

以document.getElementById（）为例，低于IE5的版本用document.all进行实现，但按实际开发中，document.getElementById（）使用频次更高。因此检测方法如下：

```javascript
function getElement(id){
    if (document.getElementById){
        return document.getElementById(id);
    }else if (document.all){
        return document.all[id];
    }else{
        throw new error("error");
    }
}
```

#### (1)安全能力检测

在检测能力是否存在的同时，可以检测是否能实现预期效果。可用typeof方法检测对象上对应的属性是否为函数（function）。

#### (2)基于能力检测进行浏览器分析

使用能力检测而非用户代理检测的原因是用户代理字符串容易被伪造。

##### 1)检测特性

按能力将浏览器归类。如需要使用浏览器的特性能力，采用集中检测所有能力而不是等到需要时再检测。

!! 双感叹号将对象转换为原值布尔值。

##### 2)检测浏览器

根据对浏览器特性的检测与已知特性对比，确认用户使用的浏览器。

##### 3)能力检测局限

随着版本更新，不支持某些方法的浏览器在后期版本会更新添加，因此对未来的版本不适用。

### 2、用户代理检测

用户代理检测通过浏览器的用户代理字符串确定使用的浏览器。用户代理字符串储存在HTTP请求的头部，在js可用navigator.userAgent进行访问。服务端通常接收用户代理字符串确认浏览器并执行操作；在客户端，通常是没有其他选项再考虑。

出现这种原因是在很长一段时间内，浏览器通过修改用户代理字符串来欺骗浏览器。

#### (1)历史

HTTP规范要求浏览器应该向浏览器发送包括浏览器名称和版本信息的字符，形如：

```
Mosaic/0.9 //标记/版本
```

#### (2)浏览器分析

##### 1)伪造用户代理

window.navigator.userAgent只读，给这个属性设置参数不会生效。

某些浏览器，可用_defineGetter_方法篡改用户代理字符串。

##### 2)分析浏览器

通过解析用户代理字符串（假设没有被修改），可知以下信息：
浏览器、浏览器版本、浏览器渲染引擎、设备类型（桌面/移动）、设备生产商、操作系统、操作系统版本

浏览器、操作系统、设备一直改变，需要经常更新，也可使用第三方用户代理解析程序。

GitHub：Bowser、UAParser、Platform.js、CURRENT-DEVICE、Google Closure、Mootools

## 三、DOM

DOM(document object model)文档对象模型是HTML和XML文档的编程接口，表示多层节点构成的文档。DOM独立于其他组分，JavaScript提供了API，通过JavaScript可添加、修改、删除页面的各个部分。

### 1、节点层级

document代表DOM文档的根节点，html是根节点下层的元素，称为文档元素（documentElement），其他元素包含在文档元素内。

#### (1)Node类型

Node接口在所有DOM节点类型都可以实现。

nodeType属性表示节点的类型，返回数值。对应的节点类型如下：

| 数值 | 类型                             |
| ---- | -------------------------------- |
| 1    | Node.ELEMENT_NODE                |
| 2    | Node.ATTRIBUTE_NODE              |
| 3    | Node.TEXT_NODE                   |
| 4    | Node.CDATA_SECTION_NODE          |
| 5    | Node.ENTITY_REFERENCE_NODE       |
| 6    | Node.ENTITY_NODE                 |
| 7    | Node.PROCESSING_INSTRUCTION_NODE |
| 8    | Node.COMMENT_NODE                |
| 9    | Node.DOCUMENT_NODE               |
| 10   | Node.DOCUMENT_TYPE_NODE          |
| 11   | Node.DOCUMENT_FRAGMENT_NODE      |
| 12   | Node.NOTATION_NODE               |

常用到的是元素节点（1）和文本节点（3）。

##### 1)nodeName与nodeValue

nodeName为元素标签名

nodeValue为node的值，text显示其内容

适用于元素节点，在使用前，先检测节点类型。

##### 2)节点关系

文档内存在子元素、父元素、同胞元素等关系。

节点包含childNode属性，其中又包含NodeList实例，是一个类数组对象。用中括号[ ]，可访问对象属性，如
childNode[0]，可用Array.prototype.slice.call(xx.childNodes,0)或Array.from(xx.childNodes)转换为数组

节点包含parentNode属性，指向父元素。chlidNodes中所有节点有同一个父元素，parentNode指向同一元素（被调用本身）。

xx.childNodes[x].previousSibling和xx.childNodes[x].nextSibling可在childNode列表内导航，当在第一个和最后一个是，返回null（特别的，当childNode只有一个属性时，均为null。）作用在本列表。

xx.childNodes[x].firstChild和xx.childNodes[x].lastChild分别访问childNodes的第一个和最后一个子节点。当childNode只有一个属性时，xx.childNodes[x].firstChild和xx.childNodes[x].lastChild为同一属性，没有均为null。

 xx.childNodes[x].ownerDocument指向存在于的文档。同一节点不能存在于多个文档中，所以可以快速访问到根节点。

##### 3)操纵节点

以上关系指针均为只读，只能进行访问，操纵节点的方法如下：

xx.childNodes[x].appendChlid（）方法接收node对象，返回node对象。用于在chlidNodes列表末尾添加节点，关系指针如父关系（parentNode）和最后子节点（lastNode）均会更新。若接收已有node对象，会移动对象位置至尾部。

xx.childNodes[x].insertBefore（）方法接收要插入的节点和参照节点，会将插入的节点置于参照节点之前，返回插入节点。

xx.childNodes[x].replaceChild（）方法接收要插入的节点和被替换节点，继承被替换的节点的所有指针。

xx.childNodes[x].removeChild（）方法接收要移除的节点。

对于替换和移除方法，节点储存于文档内，但没有位置可供读取。

以上方法均作用于xx.childNodes[x]的子节点列表中。 

##### 4)其他方法

cloneNode（）方法接收一个布尔值，返回与调用它的节点一模一样的节点，传入“true”，进行深复制，包含节点及整个DOM树，传入"false",则复制调用该方法的节点。

经此方法复制的节点归文档所有，但没有对应的父节点，称为孤儿节点（orphan），可用xx.appaendChild（）、xx.insertBefour（）、xx.replaceChild（）方法添加关联。节点添加在xx元素内

normalize（）处理文档子树的文本节点，在节点调用时会检测节点的所有后代，当发现不含文本的文本节点或者文本节点之间为同胞关系时，会删除文本节点或者合并文本节点，

#### (2)Document类型

Document表示文档节点的类型，是HTMLDocument的实例，表示整个HTML页面。document是window的一个属性，为全局对象。

子节点包含DocumentType、Element、ProcessingInstruction或comment类型

##### 1)文档子节点

documentElement访问document内的<html>元素

document.body访问<html>元素内的<body>元素

document.doctype访问DocumentType——<!DOCTYPE>

##### 2)文档信息

document.title访问<title>元素，修改title属性会反映在页面标签标题上，但不会修改title元素

document.URL取得完整URL

document.domain取得域名

document.referrer取得来源

以上三个属性只有domain可以设置，但设置的参数有限制，如：

当URL为“p2p.wrox.com”，则domain只能设置为“wrox.com”，不能设置URL不包含的值，否则会出错。

设置域名用于页面包含来自不同	子域的<frame>或者<iframe>无法通信的情况，设置相同的document.domain，页面可以访问对方的JavaScript对象。

document.domain有放松后不可回滚收紧的特性，如：

URL为“p2p.wrox.com”

先设置document.domain为wrox.com后，不能设置为p2p.wrox.com。

##### 3)定位元素

getElementById（）接收元素的Id名，返回对应元素或null（若无对应Id时）。Id名必须大小写完全匹配。多个同名Id时返回第一个。

getElementByTagName（）接收标签名（当为*时返回所有元素），返回包含多个元素的NodeList。在HTML文档中，返回HTMLCollection对象，同样可用 [ ]访问，同时提供了nameitem[ ]对有name属性的元素进行访问。综上，[ ]可键入索引值或字符串（name值）访问对应元素。

getElementByName（）接收name属性值。与getElementByTagName（）类似。name值常用于单选按钮，同一字段的单选按钮具有相同的name属性，确保多个单选按钮只有一个传入服务器。

##### 4)特殊集合

document.anchors包含文档中所有带name属性的<a>元素

document.forms包含文档中所有<from>元素

document.images包含文档中所有<img>元素

document.links包含文档中所有带href属性的<a>元素

以上集合是HTMLCollection的实例。

##### 5)DOM兼容性检测（已废弃，不推荐使用）

document.implementation.hasFeature（）方法接收特性名称和DOM版本。如果浏览器支持指定的特性和版本，指返回“true”。

##### 6)文档写入

write（"<xx>"+"xxxx"+"<xx>"）接收字符串并显示

writeln（"<xx>"+"xxxx"+"<xx>"）接收字符串，添加换行显示

用于动态包含外部资源，不能直接包含<script>标签，而要：

```JavaScript
<html>
<body>	
	<script type="text/javascript">
    	document.write("<scripr type=\"text/javascript\" src=\"filt.js\">"+"<\/script>")
	</script>
</body>
</html>
```

可以用window.onload将document.write方法设置在页面加载完后调用，则输出的内容会重写整个页面，如下

```javascript
<html>
<body>	
	<script type="text/javascript">
    	window.onload=
        document.write("<scripr type=\"text/javascript\" src=\"filt.js\">"+"<\/script>")
	</script>
</body>
</html>
```

open（）和close（）用于打开和关闭网页输出流。在调用两个write是非必须。

#### (3)Element类型

用NodeName、TagName可获取元素的标签名，返回大写字母。

##### 1)HTML元素

HTML用HTMLElement类型表示，继承了Elemen的id、title、lang、dir、classNam，可以获取对应值，也可以进行修改。

##### 2)属性

getAttribute（）、setAttribute（）、removeAttribute（）分别用于获取、设置、移除标签上的属性。

获取属性：1、未含有对应属性返回null。2、可以获取自定义的属性。3、不区分大小写。4、html5规范，自定义属性前加"date-"。5、DOM读取的元素同样带有设置的属性，但不包含自定义属性。6、对于style属性，获取属性返回css的字符串，DOM属性返回CSSStyleDeclaration对象。对于事件属性（如onclick），返回JavaScript源代码，DOM属性返回JavaScript函数。基于以上差异，开发一般用对象属性。

设置属性：setAttribute（）接收要设置的属性名、属性的值两个参数。若存在，则会代替原值。同样可以给DOM属性赋值，但自定义属性无效。

##### 3)attributes属性

attributes属性是Element类型特有的DOM属性，包含NameNodeMap实例（类NodeList）元素的每个属性都储存在对象里。

getNameItem（name）：获得属性名为name的节点

removeNameItem（name）：删除属性名为name的节点

setNameItem（node）：添加node节点，以其nodename为索引

item（pos），返回索引位置出的节点

开发者更倾向于使用2)属性的方式。attributes属性用在需迭代元素上所有属性时。

##### 4)创建元素

document.createElement（）接收被创建元素的标签名。创建的节点属于document，但为孤儿节点。可以用node类型其他方法为其添加关联。添加后立马进行渲染。

可以继续为其添加属性。

##### 5)元素后代

同一元素可以有一个或多个子元素，对于其子元素只让某一个特定部分执行操作，可用：

```JavaScript
for(let i = 0,len = document.childNodes.length ; i<len ; ++i){
    if(element.childNodes[i].nodetype == 1){
        //执行操作
    }
}
```

也可以用getelementByTagName（）方式，但会将元素包含的子元素及子元素包含的同标签元素一起捕捉。

#### (4)text类型

NodeValue返回文本字符串。

appendDate（text）：向节点末位添加text，添加text节点不会添加空格

deleteDate（offset，count）：从offset位置开始删除count个字符

insertDate（offset，text）：从offset位置插入text

replaceDate（offset，count，text）：用text替换从offset到offset+count的文本

splitText（offset）：在offset将文本节点拆成两个文本节点

substringDate（offset，count）：提取从offset到offset+count的文本

length：获取文本节点中包含的字符数量

##### 1)创建文本节点

document.createTextNode（）方法接收要插入节点的文本。（插入的文本应用HTML编码）其归属于文档document，与创建元素一致，不设置归属不进行显示。

```javascript
let element = document.createElement("div");
let textNode = document.createTextNode("hello,world!");
element.appendChild(textNode);
document.body.appendchild(element);
```

##### 2)规范化文本节点

同一标签下多个文本节点在渲染层面与单个文本节点添加同样的字符串是一致的，只提供一个动态添加文本形式，其不同在于node.length的值。在开发中，可以用xx.normalize（）方法对同胞文本节点进行合并。

##### 3)拆分文本节点

splitText（）方法接收一个数值，在此处拆分成两个文本节点，拆分位置归后一个文本节点所有。拆分后拥有同一个parentNode。

合并与拆分常用于从文本节点提取数据的DOM解析技术。

#### (5)Comment类型

注释通过Comment类型表示。

comment与text类型继承同一个基类（characterdate），拥有除splittext方法之外相同的方法。特别的，有以下：<div><!--Comment--></div>

可作为div元素节点的子节点访问comment节点。

document.createComment（）方法接收注释文本，创建注释节点。

对于<html>结束后的注释，无法被浏览器承认。

#### (6)CDATASection类型

CDATASection类型表示XML中特有的CDATA区块。

#### (7)DocuemntType类型

DocuemntType类型表示文档的文档类型。

对于支持这个类型的浏览器，documentType对象储存在document.doctype的属性中。

documentType对象包含三个属性，name（文档类型名称）、entities（文档类型描述实体的namenodemap）、notations（文档类型描述表示法的namenodemap）。html文档类型中，entities、notations为null。name属性为<!DOCTYPE后续的那串文本（html5文档类型值为html）。

#### (8)DocumentFragment（文档片段）类型

DocumentFragment类型是唯一一个在html标记中没有对应表示的类型。作为"轻量级"文档，能够包含和操作节点，却没有完整文档那样额外的消耗。其parentsnoed值为null，子节点可以是element、processinginsrtuction、comment、text、CDATASection、entityreference。

无法将DocumentFragment添加到文档，**其作用是充当其他要被添加到文档的节点的仓库。**

document.createDocumentFragment（）创建一个文档片段。

文档片段继承所有Node类型关于DOM操作的方法。

#### (9)Arrt类型

属性节点对象有name、value和specified属性，name为属性名（与noedName一致），value为属性值（与nodeValue），specified为属性使用的是默认值或被指定值的布尔值。

document.createAttribute（）方法接收属性名，创建一个属性。用法如下：

```javascript
let attri = document.createAttribube("align");
attri.value = "left";
element.setAttributeNode("attri");
```

### 2、DOM编程

操作DOM可通过HTML或JavaScript进行实现。

#### (1)动态脚本

动态脚本是指页面初始加载时不存在，之后通过修改DOM动态添加的脚本。与直接在页面内的<script></script>相反。·有引入外部文件和直接插入源代码两种方式。

```javascript
//引入外部文件
//直接添加
<script src="javaScript.js"></script> 
//动态脚本
let script = document.createElement("script");
script.src = "javaScript.js";
doocument.body.appendChild(script); //也可以添加节点到head标签
//函数化动态脚本
function loadscript(url){
    let script = document.createElement("script");
	script.src = url;
    doocument.body.appendChild(script);
}
//应用函数
loadscript(javaScript.js);

//插入源代码
//直接添加
<script>
    function sayhi(){
    	alert("hi");
	}
</script>
//动态脚本
//不支持IE低版本
var script = document.createElement("script");
var textnode = document.createTextNode('function sayhi(){alert("hi");}');
script.appendChild(textnode);
doocument.body.appendChild(script);
//不支持safari3之前的版本
var script = document.createElement("script");
script.text = 'function sayhi(){alert("hi");}';
doocument.body.appendChild(script);
//适配版本
var script = document.createElement("script");
var	text = 'function sayhi(){alert("hi");}';
try{
    script.appendChild(document.createTextNode(text);
}catch(ex){
    script.text = text;
    }
doocument.body.appendChild(script);
//函数化源代码适配版本动态脚本
function loadscript(text){
    var script = document.createElement("script");
    script.type = "text/javascript";
    try{
    	script.appendChild(document.createTextNode(text);
}catch(ex){
   		script.text = text;
    }
    doocument.body.appendChild(script);
}
//应用函数
loadscript('function sayhi(){alert("hi");}');
```

通过innerHTML属性创建的<script>元素不会执行。

#### (2)动态样式

动态样式与动态脚本类似，在页面初始加载时并不存在，在之后才添加到页面中。跟样式加载到页面的方式一致，有外部添加、内部添加、行内添加之分。

```javascript
//外部添加
let link = document.createElement("link");
link.rel = "stylesheet";
link.type = "text/css"
link.href = "style.css";
let head = getElementByTagName("head")[0];
head.appendchild(link);
//省略函数化
//内部添加
let style = documen.creatElement("style");
style.type = "text/css"; 
//IE早期版本采用：style.stylesheet.cssText = "body{background:red;}"
let csstext = document.createTextNode("body{background:red;}");
let style = document.appendChild(csstext);
let head = getElementByTagName("head")[0];
head.appendChild(style);
//省略函数化
```

在IE中，styleSheet.cssText如果重用同一个<style>元素并设置该属性超过一次，可能导致浏览器崩溃，设置为空字符串也可能导致浏览器崩溃。

#### (3)操作表格

利用DOM编程创建修改表格若按HTML原本的格式进行会十分繁琐。因此，HTML DOM给<table>、<tbody>、<tr>元素添加了一些属性和方法。

1、<table>包括如下属性及方法：caption（指向<caption>的指针）、tBodies（包含tbody的HTMCollection）、tFoot（指向<tFoot>的指针）、tHead（指向<thead>的指针）、rows（包含表示所有行的HTMCollection）、

createTHead( )（创建<thead>元素，放在表格中，返回引用）、

createTFoot( )（创建<tfoot>元素，放在表格中，返回引用）、

createCaption( )（创建<caption>元素，放在表格中，返回引用）、

deleteTHead( )（删除<thead>元素）、deleteTFoot( )（删除<tfoot>元素）、

deleteCaption( )（删除<caption>元素）、deleteRow(pos)（删除给定位置的行）、

insertRow(pos)（在行集合中给定位置插入一行）

2、<tbody>包括如下属性及方法：rows（包含<tbody>元素中所有行的HTMCollection）、

deleteRow(pos)（删除给定位置的行）

insertRow(pos)（在行集合中给定位置插入一行）

3、<tr>包括如下属性及方法：cells（包含<tr>元素所有标元的HTMCollection）、deletCell(pos)（删除给定位置的表元）、insertCell(pos)（在表元集合给定位置拆入一个表元，返回该表元的引用。）

| cell1,1 | cell2,2 |
| ------- | ------- |
| cell1,2 | cell2,2 |

对于如上表格，运用HTML DOM属性方法如下：

```JavaScript
let table = document.createElement("table");
table.border = "1";
table.width = "100%";
//创建表体
let tbody = document.createELement("tbody");
table.appendChild(tbody);
//创建第一行
tbody.insertRow(0);
tbody.Rows[0].insertCell(0);
tbody.Rows[0].Cells[0].appendChild(document.appendTextNode("cell1,1"));
tbody.Rows[0].insertCell(1);
tbody.Rows[0].Cells[0].appendChild(document.appendTextNode("cell2,1"));
//创建第二行
tbody.insertRow(1);
tbody.Rows[1].insertCell(0);
tbody.Rows[1].Cells[0].appendChild(document.appendTextNode("cell1,2"));
tbody.Rows[1].insertCell(1);
tbody.Rows[1].Cells[1].appendChild(document.appendTextNode("cell2,2"));
//添加到主体
document.body.appendChild(table);
```

#### (4)NodeList

NodeList对象和相关的NamedNodeMap、HTMLCollection三个集合类型是实时响应的，文档结构的变化会即时变现出来。

使用appendElement(element)会使对应NodeList.length + 1 。因此，在调用实时性对象或集合循环时，最好将当前NodeList.length给到变量，用变量参与循环。或者反向迭代如：(for i=NodeList.length -1 ; i >=0 ; --i)。

t子节点、文本，以及三者任意组合的变化。

### 3、MutationObserver接口

MutationObserver接口，可以在DOM被修改时异步执行回调。可以观察整个文档、DOM树的一部分，或某个元素，或元素属性、子节点、文本，以及三者任意组合的变化。

#### (1)基本用法

##### 1)observe（）

可以用构造函数的方式创建MutationObserver接口，接收一个将会异步执行注册的回调函数。

observe（）方法接收 要观察的节点 和 MutationObserverInit对象。MutationObserverInit对象是一个键/值形式的参数。

```javascript
let observer = new MutationObserver(function());
observer.observe(document.body,{attributes:true});//监测document.body节点上属性变化
```

##### 2)回调和MutationObserverInit

用observe（）方法监测观察的节点发生MutationObserverInit对象包含的变化，“后”执行回调函数，每次回调创建MutationRecord实例的数组，记录每次变化的内容。（多次回调形成）

```javascript
let observer = new MutationObserver((mitationRecords)=>console.log(mitationRecords));
observer.observe(document.body,{attributes:true});
document.body.setAttribute("foo","bar");

//addedNodes: NodeList []
//attributeName: "foo"      //传入的属性名
//attributeNamespace: null
//nextSibling: null
//oldValue: null
//previousSibling: null
//removedNodes: NodeList []
//target: body             //传入的属性值
//type: "attributes"       //变化的类型
```

MutationInit实例的属性

| 属性                           | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| addedNodes                     | 针对childList变化，返回包含**变化中添加节点**的NodeList。其他类型变化值为null。 |
| attributeName（属性名）        | 对于attributes变化，保存被修改属性的名字。默认值为null。     |
| attributeNamespace（命名空间） | 对于使用了命名空间"Attributes"的变化，保存被修改属性的名字，其他类型变化为null。 |
| nextSibling（）                | 针对childList变化，返回**变化节点**的后一个同胞节点。默认值为null。 |
| oldValue（）                   | 若MutationIObserverInit对象含有{attributeOldValue:true}或{characterDate OldValue:true}，“attributes”或“characterDate”的变化事件会设置这个属性为被替代之前的值。 |
| previousSibling                | 针对childList变化，返回**变化节点**的前一个同胞节点。默认值为null。 |
| removedNodes                   | 针对childList变化，返回包含**变化中删除节点**的NodeList。其他类型变化值为null。 |
| target                         | 被影响的目标节点。                                           |
| type                           | 字符串，表示变化的类型“attributes”、“characterDate”、“childList”。 |

##### 3)disconnect（）方法

disconnect（）方法用于提前终止执行回调，不仅停止下一步变化事件的回调，同时移除了之前加载入任务队列异步执行的回调。如下：

```javascript
let observer = new MutationObserver(()=>console.log("continue"));
observer.observe(doucment.body,{attributes:true});
document.body.setAttribute("foo","bar");
observer.disconnect();
document.body.foo = "far";
//没有输出，打断后一个回调并移除队列里的回调。
```

可以用setTimeout（）让已经入列的回调执行，如下：

```JavaScript
document.body.setAttribute("foo","bar");
setTimeout(()=>{
    observer.disconnect();
document.body.foo = "far";
},0;
)
//document.body.setAttribute("foo","bar")触发执行回调
```

##### 4)复用MutationObserver

多次调用observe（）方法，可以复用一个MutationObserver对象观察不同的目标节点，在target属性中标识发生变化事件的目标节点。

```javascript
let observer = new MutationObserver(
//mutationRecords、x作为函数的参数，自定义
    (mutationRecords)=>console.log(mutationRecords.map((x)=>x.target))
);
//向页面添加两个节点
let childA = document.createElement("div");
let childB = document.createElement("span");
document.body.appendChild(childA);
document.body.appendChild(childB);
//观察两个节点
observer.observe(childA,{attributes:true});
observer.observe(childB,{attributes:true});
//修改两个子节点的属性
childA.setAttribute("foo","bar");
childB.setAttribute("foo","bar");
```

调用disconnect（）方法会停止观察所有目标。

##### 5)重用MutationObserv
	调用disconnect（）方法不会接收MutationObserver的生命。可以将Observer重新关联到新的（或者原来的）目标节点。

```javascript
//连接设置一次关联
setTimeout{()=>{
    observer.disconnect();
    //下行代码不会触发变化事件
    document.body.setAttribute("bar","baz");
},0};
setTimeout{()=>{
    //重关联
    observer.observe(document.body,{attribute:ture});
    //这行代码会触发变化事件 
    document.body.setAttribute("baz","qux");
},0);
```

#### (2)MutationObserverInit与观察范围

MutationObserverInit对象用于控制对目标节点的观察范围。

MutationObserverInit对象的属性

| 属性                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| subtree               | 布尔值，表示除了目标节点，是否观察目标节点的子树（后代），默认为false。 |
| attributes            | 布尔值，表示是否观察目标节点的属性，默认为false。            |
| attributeFilter       | 字符串数组，表示要观察哪些属性的变化。把值设置为true会将attributes的值转换为true。默认观察所有属性。 |
| attributeOldValue     | 布尔值，表示MutationRecord是否记录变化之前的属性值。把值设置为true会将attributes的值转换为true。默认为false |
| characterDate         | 布尔值，表示修改字符数据是否触发变化事件。默认是false        |
| characterDateOldValue | 布尔值，表示MutationRecord是否记录之前的字节数据。把值设置为true会将characterDate的值转换为true。默认为false |
| childList             | 布尔值，表示修改目标的子节点是否触发变化事件。默认为false。  |

在调用observe（）方法时，attributes、characterDate、chlidList属性必须至少有一项为真（包括设置其他属性导致以上属性为真），否则会抛出错误。

##### 1)观察属性

```javascript
{attributes:true}
{attributeFilter:["foo","boo"]}//添加入白名单
{attributeOldValue:true}
```

设置观察属性变化，包括添加、修改、删除属性。

可以用attributeFilter观察包含在数组内的属性的变化。

设置attributeOldValue可以将本次修改属性的上一次属性值返回。特别的，当首次添加属性到节点时，由于上一次未存在，因此返回"null"。

##### 2)观察字符数据

```javascript
{characterDate:true}
{characterDateOldValue:true}
```

设置观察文本节点变化（如text、comment或ProcessingInstruction节点），包括添加、修改、删除文本。

设置characterDateOldValue可以将本次修改文本的上一次文本字符数据返回。特别的，当首次添加文本到节点时，由于上一次未存在，因此返回"null"。 

##### 3)观察子节点

```javascript
{childList:true}
//设置观察对象，创建两个初始子节点在ChildList中。
//调用insertBefore方法交互两个子节点。
document.insertBfore(document.body.lastChild,document.body.firstChild,)
//返回两次回调函数。
```

设置观察目标节点的子节点变化，包括添加、移除子节点（appendChild、removeChild方法）。

对子节点重现排序会报告两次变化事件。

##### 4)观察子树

```javascript
{subtree:true}
```

设置观察的范围扩展到对应节点的子树（所有后代节点）。

对于被移出子树的被观察子树的节点，仍然能触发变化事件。

#### (3)异步回调与记录队列

##### 1)记录队列

MutationRecord被添加到MutationObserver的记录队列时，仅当之前没有已排期的微任务回调时（队列中微任务长度为0），才会将观察者注册的回调（在初始化MutationObserver时传入）作为微任务调度到任务队列上。

回调的微任务异步执行期间，被调用的回调会接收并处理一个MutationRecord实例的数组，顺序为进入记录队列的顺序。处理后函数退出实现就不存在。回调执行后，MutationRecord用不着，因此记录队列会被清空，其内容会被丢弃。

##### 2)takeRecords（）方法

调用MutationObserver实例的takeRecord（）方法可以清空记录队列，取出并返回其中所有的MutationRecord实例，如下：

```javascript
//回调函数设置为((MutationRecord)=>{console.log(MutationRecord)})
//设置观察对象{Attributes:true},触发三次变化事件
console.log(observe.takeRecord());
console.log(observe.takeRecord());
//返回三个回调记录
//返回空数组（取出后清空）
```

方法用于断开与观察目标又希望处理用于调用disconnect（）方法而被抛弃的记录队列中的MutationRecord实例。

#### (4)性能、内存与垃圾回收

##### 1)MutationObserver的引用

MutationObserver实例对目标节点的引用为弱引用，不会妨碍垃圾回收程序回收目标节点。

目标节点对MutationObserver实例的引用为强引用，目标节点移除后被垃圾回收，关联的MutationObserver也会被垃圾回收。

##### 2)MutationRecord的引用

被记录MutationObserver实例根据target类型不同，会包含DOM节点至少一个引用（childList对应多个）。回调默认行为是耗尽记录队列，处理后让它们超出作用域并被垃圾回收。

保存MutationRecord实例也会保存引用的节点，会防止节点回收。如需尽快释放内存，建议提取MutationRecord中有用的信息，保存至新对象，最后抛弃MutationRecord。

## 四、DOM扩展

### 1、Selector API

Selector API规定了浏览器原生支持CSS查询API，即根据CSS选择符的模式匹配DOM元素，替代getElementById（）和getElementByTagName（）方法。包含querySelector（）和querySelectorAll（）方法，方法可用于document、Element。支持css选择器。

#### (1)querySelector（）

querySelector（）接收css选择符参数，返回匹配该模式的第一个后代元素，没有匹配的返回null。

（包括标签选择“div”、类选择“.class”、id选择“#id”）

document上使用时从文档元素开始搜索，element上使用时只会从当前元素的后代中查询。

#### (2)querySelectorAll（）

与querySelector（）一致，但返回包含满足选择要求的ChidList，没有则返回空数组。

#### (3)matchse（）

matchse（）方法接收一个css选择符参数，如果元素匹配则选择器返回true，否则返回false。

使用该方法可以验证元素是否能被以上方法返回，

### 2、元素遍历

元素间的空格在ie9之前的版本不会被当为空白节点，但其他浏览器会。这导致了childNodes和firstChild等属性的差异。为了弥补这个差异，通过新的ElementTraversal定义了属性，作用于DOM元素。

childElementCount，返回子元素数量（不包含文字节点和注释）

firstElementChild，指向第一个元素节点，与firstChild类似。

lastElementChild，指向最后一个元素节点，与lastChild类似。

previousElementSibling，指向目标元素前一个同胞元素节点，与previousSibling类似

nextElementSibling，指向目标元素后一个同胞元素节点，与nextSibling类似

方法摆脱了空白节点的困扰。

### 3、HTML5

HTML5提供了与标记相关的JavaScript的API定义，有些定义了DOM扩展。

#### (1)css类扩展

##### 1)getElementByClassName（）

getElementByClassName（）方法接收一个或多个类名的字符串，返回相应类名元素的NodeList（包括子树内的所有同类名元素），作用于document对象和所有元素对象上。

```javascript
//返回类名为username current的元素
document.getElementByClassName("username current");
```

##### 2)classList属性

HTML5之前操作类名，需要通过className属性实现，经切片、寻找检索、删除、重新设置类名后完成。

HTML5对所有元素增加classList属性，是集合类型DOMTokenList的实例。DOMTokenList有length属性，可以通过item（）或 [ ] 获取个别元素。同时对数列包含以下方法：

add(value)：向类名列表中添加指定的字符串值value，如存在则不变。

contains(value)：返回布尔值，表示给定的value是否存在。

remove(value)：从类名列表中删除指定字符串值value。

toggle(value)：如类名已存在指定value，则删除；若不存在，则添加。

如此，操作类名可简化为：

```javascript
div.classList.remove("user");
```

#### (2)焦点管理

增加辅助DOM焦点管理功能：document.activeElement。属性始终包含当前拥有焦点的DOM元素。

Element.focus（）方法设置element为焦点。

document.hasfocus（）接收一个元素节点，返回布尔值，表示是否拥有焦点。

#### (3)HTMLDocument扩展

##### 1)readystate属性

document.readystate属性返回两个两个值：loading（表示文档正在加载）/complete（表示文档加载完成）。

开发中常作为指示器判断文档是否加载完毕，如下：

```javascript
if(document.readystate =="complete"){
	//执行操作
}
```

##### 2)compatMode属性

document.compatMode指示浏览器当前处于 标准模式（返回：CSS1Compat）或是混杂模式（返回：BackCompat）

##### 3)head属性

HTML5把文档的head标签指向标准化。

document.head指向文档的<head>元素。

#### (4)字符集属性

document.characterSet属性表示文档使用的字符集，也可以设置新字符集。默认为UTF-16。可通过<mete>属性和characterSet属性修改。

#### (5)自定义数据属性

可以给元素指定非标准的属性，需要使用前缀 ”data-“ 。这些属性不包含与渲染有关的信息，也不包含元素的语义信息。

定义了自定义数据属性后可通过元素的dataset属性访问。dataset属性是一个DOMStringMap实例，包含一组值/对映射。data-name属性在dataset可以用data-后面的字符串作为键来访问。

自定义数据属性适用于需要给元素附加某些数据的场景，如链接追踪和在聚合应用程序中标识页面不同部分，也用于单页应用程序框架中。

#### (6)插入标记

##### 1)innerHTML属性

读取innerHTML属性返回目标元素所有后代的HTML字符串，包括元素、注释和文本节点。写入时根据字符串替换掉原来元素包含的所有节点，如没有标签则插入文本节点。（写入字符串格式为HTML。）

##### 2)旧版本IE的innerHTML

##### 3)outerHTML属性

读取)outerHTML属性返回目标元素及所有后代的HTML字符串（与innerHTML的不同点），写入时替换本身及后代节点。

##### 4)insertAdjacentHTML（）和insertAdjacentText（）

insertAdjacentHTML（）和insertAdjacentText（）方法接收要插入标签的位置和要插入的HTML或文本两个参数。第一个参数必须是以下其中一个值：
"beforbegin"：插入当前元素前边，作为前一个同胞节点

"afterbegin"：插入当前元素内部，作为新的子节点或者在第一个子节点前面

"beforeend"：插入当前元素内部，作为新的子节点或者在最后一个子节点后面

"afterbend"：插入当前元素后边，作为后一个同胞节点

当是HTML时，会在解析出错时抛出错误。

##### 5)内存与性能问题

使用以上涉及的属性和方法操作节点会由于事件关联或JavaScript对象引用的关系滞留在内存中（当移除时），频繁操作导致内存占用攀升。因此使用前最好手动删除被替换元素关联的事件处理程序和JavaScript对象。

同时应该控制innerHTML和outerHTML的次数，不进行循环。

##### 6)跨站点脚本

使用innerHTML暴露了很大的攻击面，特别对于页面要使用到用户的信息，用innerHTML传入极易遭受xss攻击，需要隔离要插入的数据，用相关库进行转义。

#### (7)scrollIntoView（）

scrollIntoView（）方法存在于所有HTML元素上，可以滚动浏览器窗口或容器元素一遍包含元素进入视口。参数如下：

alignToTop是一个布尔值。"true"：窗口滚动后元素的顶部与视口顶部对其。"false"：窗口滚动后元素的地步与视口底部对齐。

scrollIntoViewOpotions是一个选项对象。

"behavior"：定义过渡动画，有"smooth"、"auto"可选，默认为"auto"。

"block"：定义垂直方向的对齐，有"start"、"center"、"end"、"nearest"，默认为"start"。

"inline"：定义水平方向的对齐，有"start"、"center"、"end"、"nearest"，默认为"nearest"。

### 4、专有扩展

#### (1)children属性

IE9之前版本与其他浏览器在处理空白文本节点上的差异导致children属性出现。

children是一个HTMLCollection，只包含元素的Element类型的子节点。

#### (2)contains（）方法

contains（）方法接收一个目标节点，应用于要搜索的元素上，判断目标节点是否在被搜索的元素上。

compareDocumentPosition（）方法也可以确认节点关系。会返回表示两个节点关系的位掩码。

| 掩码 | 节点关系                             |
| ---- | ------------------------------------ |
| 0x1  | 断开（目标节点不在文档中）           |
| 0x2  | 领先（目标节点在被搜索节点之前）     |
| 0x4  | 随后（目标节点在被搜索节点之后）     |
| 0x8  | 包含（目标节点是被搜索节点的祖先）   |
| 0x10 | 被包含（目标节点是被搜索节点的后代） |

#### (3)插入标记

innerText，读取子树的文本并按深度优先的顺序将文本凭借起来。写入时移除元素的所有后代写入一个文本节点。

outerText，参照innerText，但包含调用的元素。

#### (4)滚动

其他浏览器有专用控制滚动的扩展，但scrollIntoView（）所有浏览器均支持。

## 六、事件

JavaScript与HTML的交互通过事件实现。事件代表文档或浏览器窗口中某个有意义的时刻，可以使用仅在事件发生时执行的监听器订阅事件。以上触发模型叫“观察者模式”。

可以做到页面行为（js定义）和页面展示（HTML、CSS定义）分离。

### 1、事件流

事件流描述页面接收事件的顺序（假设HTML节点嵌套，从内部节点到外部节点或从外部节点到内部节点触发的顺序视为接收事件的顺序）。IE支持事件冒泡流，Netscape支持事件捕获流。两种方案截然不同。

#### (1)事件冒泡

事件冒泡指事件顺序由内部向外部扩大，由具体元素向上层元素触发。

现代浏览器支持事件冒泡，一直冒泡至window对象。

#### (2)事件捕获

事件捕获指最大包容节点最先触发，并往下传播。

现代浏览器支持事件捕获，但由于旧版本浏览器不支持，因此实际不会使用事件捕获。

#### (3)DOM事件流

规范规定事件流分为三个阶段：事件捕获、到达目标、事件冒泡。条件捕获开始，为提前拦截时间提供了可能，实际目标元素接收到事件，事件冒泡最后，最迟在此阶段响应时间。

### 2、事件处理程序

#### (1)HTML事件处理程序

在HTML的事件处理程序形如：

```html
<input type="button" onclick="console.log('abc')"/>
<input type="button" onclick="console.log(this.type)"/> //返回input的type属性值“button”
```

事件名前添加on，作为属性添加入标签中。值为执行的代码，可以以行内格式、内部引用和外部引用实现，可以访问全局作用域的一切。

通过HTML方式创建的事件处理程序有特殊的地方。会创建一个函数封装onclick的值，这个函数有一个特殊的局部变量event，保存event对象。

行内的this指向目标元素。

创建的函数的作用域扩展，可以往上访问（一直到document），通过with（）实现。即可以快速访问到同胞或父节点的属性（通过name的值访问）。

由HTML创建的执行代码，必须要在被触发前被定义，否则抛出JavaScript错误，常见用try/catch(ex)封装，在报错前拦截。

#### (2)DOM0事件处理程序

JavaScript中指定事件处理程序是从赋值给属性层面进行。

```javascript
//假设存在<input type="button" id="mybtn"/>
let btn = document.getElementById("mybtn");
btn.setAttribute("onclick");
btn.onclick = function() {
    console.log("click!") //console.log(this.id)返回mybtn
}
```

函数内部this指向目标元素。可访问元素的属性及方法。

将onclick赋值null，即可移除添加的事件处理程序，适用于HTML类型。

#### (3)DOM2事件处理程序

addEventListener（）、removeEventListener（）方法：接收 事件名、事件处理函数、布尔值三个参数，用于所有DOM节点，true表示在捕获阶段调用事件处理程序，false（默认值）表示在冒泡阶段调用事件处理程序。

```javascript
let btn = document.getElementById("mybtn");
btn.addEventListener("click",()=>{
    console.log(this.id)
},false);
```

使用DOM2的优势是可以为同一个事件添加多个处理程序。当同一事件触发函数时，以添加的顺序来触发。

由addEventListener（）方法添加的事件处理程序需要用removeEventListener按相同参数移除，事件处理函数用匿名函数无法被移除。

大部分事件处理程序被注册至冒泡阶段，其兼容性好，注册至捕获阶段通常用于在事件到达目标节点前拦截。

#### (4)IE事件处理程序

attachEvent（）、detachEvent（）方法接收 事件处理程序的名字、事件处理函数。使用attachEvent（）添加的程序只会添加到冒泡阶段。

在IE事件处理程序与DOM0事件处理程序中，主要区别是事件处理程序运行的作用域不同，IE运行在全局作用域。

attachEvent（）也可以为同一事件添加多个处理程序，与addEventListener（）不同，按添加它们的反向触发，即后进先出。

#### (5)跨浏览器事件处理程序

先用DOM2、IE，最后检测DOM0（兼容性最低）。·	

```JavaScript
//用一个对象包含两个函数分类添加和移除事件处理程序
var EventUitl ={
	addhandler:function(element,type,handler){
		if(element.addEventListener){
			element.addEventListener(type,handler,false);
		}else if(element.attachEvent){
			element.attachEvent("on"+type,handler);
		}else{
			element["on"+type] = handler;
		}
	},
	removehandler:function(element,type,handler){
		if(element.removeEventListener){
			element.removeEventListener(type,handler,false);
		}else if(element.detachEvent){
			element.detachEvent("on"+type,handler);
		}else{
			element["on"+type] = null;
		}
	}
};
//引用似例
let elementbtn = document.createElement("button");
document.body.appendChild(elementbtn);
elementbtn.setAttribute("id","mybtn");
elementbtn.appendChild(document.createTextNode("点击！"))
let btn = document.getElementById("mybtn");
let printId = function(){console.log(this.id)};//必须为一个函数
EventUitl.addhandler(btn,"click",printId);
```

### 3、事件对象

DOM发生事件时，所有相关信息都会收集在event对象中，包含 导致事件的元素、发生的事件类型，以及可能与特定事件相关的任何其他数据。例如，鼠标操作导致的事件会生成鼠标位置信息，而键盘操作导致的事件会生成与被按下的键有关的信息。

#### (1)DOM事件对象

DOM合规浏览器中，event对象是传给事件处理程序的唯一参数。（无论使用DOM0，还是DOM2方式）

事件包含的属性及方法如下：

| 属性/方法                  | 类型         | 读/写 | 说明                                                         |
| -------------------------- | ------------ | ----- | ------------------------------------------------------------ |
| bubbles                    | 布尔值       | 只读  | 表示事件是否冒泡                                             |
| cancelable                 | 布尔值       | 只读  | 表示是否可以取消事件的默认行为                               |
| currentTarget              | 元素         | 只读  | 事件处理程序所在的元素                                       |
| defaultPrevented           | 布尔值       | 只读  | true表示调用preventDefault（）方法（DOM3事件新增）           |
| detail                     | 整数         | 只读  | 事件相关的其他信息                                           |
| eventPhase                 | 整数         | 只读  | 表示调用事件处理程序的阶段：1、代表捕获阶段；2、代表到达目标；3、代表冒泡阶段 |
| preventDefault()           | 函数         | 只读  | 用于取消事件的默认行为，只有cancelable为true才可以调用这个方法 |
| stopImmediatePropagation() | 函数         | 只读  | 用于取消后续事件捕获或事件冒泡，并阻止调用任何后续事件处理程序（DOM3事件新增） |
| stopPropagation()          | 函数         | 只读  | 用于取消所有后续事件或事件冒泡。只有bubbles为true才可以调用这个方法 |
| target                     | 元素         | 只读  | 事件目标                                                     |
| trusted                    | 布尔值       | 只读  | true表示事件是由浏览器生成的。false表示事件是开发者通过js创建的（DOM3 事件新增，如vue自定义事件） |
| type                       | 字符串       | 只读  | 被触发的事件类型                                             |
| View                       | AbseractView | 只读  | 与事件相关的抽象视图。等于事件所发生的window对象。           |

- 事件处理程序中，this的对象是currentTa的值(事件处理程序所在位置)，target为事件目标(事件触发所在的位置)。如果事件处理程序直接添加在事件目标上，则this、currentTarget、target的值一致。如：添加在button上的由本标签click触发的事件处理程序。
- 当onclick事件处理程序添加至button所在body中时，点击button，click事件会冒泡至body上才触发事件处理程序。在此例子中，target为button(事件发起者)，currentTarget为body(事件处理程序所在位置)
- type属性用于一个处理程序处理多个事件，用switch语句，将event.type的不同值case不同的操作。
- preventDefault（）方法阻止特定事件的默认动作。如点击<a>标签时自动跳转到href链接，用event.preventDefaule()取消。通过该方法取消的事件，其event对象的cancelable属性都会设置为true。
- stopPropagation（）方法用于阻止事件流在DOM结构中传播。以click事件处理程序添加至button所在body中 为例，在button本身的click事件处理程序中添加event.stopPropagation()，当click时，button上的事件处理程序会触发，而body上的事件处理程序不会触发（取消传播）
- eventPhase属性确认当前事件处理程序在事件流中的阶段。通过DOM2添加事件程序并传布尔值为true，在event.eventPhase会返回1（捕获阶段）；事件目标的事件处理程序会返回2（事件自身）；通过DOM0和DOM2添加事件程序并传布尔值为false，会返回3（冒泡阶段）

#### (2)IE事件对象

IE事件对象基于事件处理程序被指定的方式以不同方式来访问。事件处理程序使用DOM0定义，则event对象只是window对象的一个属性。若使用attachEvent（）指定，则event对象会作为唯一的参数传给处理函数。

IE事件对象包含以下所列的公共属性和方法：

| 属性/方法    | 类型   | 读/写 | 说明                                                         |
| ------------ | ------ | ----- | ------------------------------------------------------------ |
| cancelBubble | 布尔值 | 读/写 | 默认为false，设置为true可以取消冒泡（与DOM的stopPropagation()方法相同） |
| returnValue  | 布尔值 | 读/写 | 默认为true，设置为false可以取消事件默认行为（与DOM的preventDefault()方法相同） |
| srcElement   | 元素   | 只读  | 事件目标（与DOM的target属性相同）                            |
| type         | 字符串 | 只读  | 触发的事件类型                                               |

事件处理程序的作用域取决于指定它的方式，因此this不总是指向事件目标（与DOM类似）。因此，指代事件目标最好用srcElement代替this。

#### (3)跨浏览器事件对象

同事件处理程序一样，可通过定义函数的方式获取兼容多种浏览器的事件对象

```JavaScript
var EventUtil = {
    getEvent: function(event){
        return event ? event : window.event; 
        //三元运算符，等同与
        //if(event){
        //	return event
    	//}else{
        //	window.event
   		//}
    },
    getTarget: function(event){
        return event.target||event.scrElement;// 或运算符
    },
	preventDefault: function(){
        if(event.preventDefault){
            event.preventDefault()
        }else{
            event.returnValue = false;
        }
    },
	stopPropagation: function(event){
        if(event.stopPropagation){
            event.stopPropagation();
        }else{
            event.cancelBubble = true;
        }
    }
}
//使用跨浏览器事件对象eventutil实例
btn.onclick = function(event){	//事件处理程序必须接收event对象。
    event = EventUtil.getEven(event)
}
```

getEvent（）方法的前提是事件处理程序必须接收event对象。

### 4、事件类型

DOM3Events定义以下类型事件：

用户界面事件（涉及与BOM交互的通用浏览器事件）、

焦点事件（元素获得或者失去焦点触发，用tab切换的焦点）、

鼠标事件（使用鼠标在页面上执行某些操作时触发）、

滚轮事件（使用鼠标滚轮（或类似设备）时触发）、

输入事件（向文档中输入文本时触发）、

键盘事件（使用键盘在页面上执行某些操作时触发）、

合成事件（使用某种IME输入字符时触发）

除此之外，HTML5还定义了另一组事件，而浏览器通常在DOM和BOM上实现专有事件。

#### (1)用户界面事件

load：在整个页面加载完成后触发。

unload：在文档卸载完成后触发。一般是从一个页面导航到另一个页面触发。

resize：浏览器窗口被缩放至新高度或新宽度时（最大化和最小化俊辉触发）。

scroll：用户滚动包括滚动条的元素时在元素上触发（整个页面或者一部分页面）

#### (2)焦点事件

blur：当元素失去焦点时触发，事件不冒泡。

focus：当元素获得焦点时触发，事件不冒泡。

focusin：当元素获得焦点时触发，focus事件的冒泡版。

focusout：当元素获得焦点时触发，blur事件的通用版。

当焦点从页面从一个元素转移到另一元素时，依次触发一下事件：

focusout（失去焦点元素触发）——focusin（获得焦点元素触发）——blur（失去焦点元素触发）——focus（获得焦点元素触发）

#### (3)鼠标、滚轮事件

click：单击鼠标左键或按键盘回车时触发

dblclick：双击鼠标左键。

mousedown：在用户按下任意鼠标键时触发。

mouseenter：鼠标光标从元素外部移到元素内部时触发，事件不冒泡，经过后代元素不触发。

mouseleave：鼠标光标从元素内部移到元素外部时触发，事件不冒泡，经过后代元素不触发。

mousemove：鼠标光标在元素是上移动时反复触发。

mouseout：鼠标光标从一个元素移动到另一元素上触发。另一个元素可以是原始元素的外部元素，也可以是其子元素。

mouseover：鼠标光标从元素外部移到元素内部时触发。

mouseup：在用户释放鼠标键时触发。

mousewheel：滚轮滑动触发



以上事件除了mouseenter和mouseleave外，其他均可以冒泡。

事件之间存在关系，click事件的前提时mousedown被触发，随后在同元素触发mouseup，如两者其一被取消，则click不触发。同理dblclick也一样。

双击某一元素的事件顺序如下：

mousedown——mouseup——click——mousedown——mouseup——click——dblclick

修饰符shift、ctrl、alt、meta，按住时触发会修改鼠标事件的行为。

#### (4)键盘、输入事件

keydown：用户按下键盘某个键触发，持续按住持续触发

keyup：用户释放键盘某个键触发。

textInput：文本被插入到文本框之前触发

### 5、内存与性能

#### (1)事件委托

过多事件处理程序的解决方案是使用事件委托，可利用事件冒泡，可以只使用一个事件处理程序管理一种类型的事件。如click事件会冒泡到document上，这样的话可以为整个页面指定一个onclick事件处理程序，而不用为每个可点击元素分别指定事件处理程序。例：

```html
<!--假设现有以下结构-->
<ul id='myul'>
    <li id='sayhello'>hello</li>
    <li id='sayworld'>world</li>
    <li id='sayhi'>hi</li>
</ul>
```

```javascript
//可使用一个事件处理程序进行操作
let ul = document.getElementById('myul')
ul.addeventlistener('click',()=>{
    let target = event.target
    switch(target.id){
        case 'sayhello':
            console.log('hellobeclicked');
            break;
        case 'sayworld'
            console.log('worldbeclicked');
            break;
        case 'sayhi'
            console.log('hieclicked');
            break;    
    }
});
```

建议在页面进行事件委托的有click、mousedown、mouseup、keydown

#### (2)删除事件处理程序

性能下降的原因大都由于无用的事件处理程序长驻内存导致。长驻内存的原因：1、用removechild（）或者replacechild（）删除了带有事件处理程序的元素。解决方法：在删除元素前移除事件处理程序。2、页面卸载。解决方法：在unloda事件处理程序中趁页面未卸载删除所有事件处理程序。

## 七、表单脚本

### 1、表单基础

web表单在html中以<form>元素存在，在js以HTMLformelement类型表示。HTMLformelement类型继承htmlelement类型，拥有与其他html元素一样的默认属性，也存在自己的属性和方法：

acceptcharset：服务器可以接收的字符集，等价于HTML的accept-charset属性。

action：请求的URL，等价于HTML的action属性。

elements：表单中所有控件的HTMLCollection。

enctype：请求的编码类型，等价于HTML的enctype属性。

length：表单中控件的数量。

method：http请求的方法类型，通常是“get”和“post”，等价于HTML的method属性

name：表单的名字，等价于HTML的name属性。

reset（）：把表单字段重置为各自的默认值。

submit（）：提交表单。

target：用于发送请求和接收响应的窗口的名字，等价于HTML的target属性。

对<form>元素的引用。（1）将表单元素作为普通元素添加id属性，通过getelementbyid（）获取表单。

（2）document.form集合可以获取页面上所有的表单元素，之后用索引值或者name属性来访问。

#### (1)提交表单

表单通过用户点击提交按钮或图片按钮进行提交。提交按钮需要设置type属性为”submit“的<input>或<button>元素来定义，图片按钮可以设置type属性为”image“的<input>元素来定义。通过此方法提交的表单会产生submit事件，可以添加事件处理程序阻止表单。

```javascript
//假设存在id名为myform的表单
let form = getElementById('myform');
form.addeventlistener('submit',(event)=>{
	event.preventDefault();
});
//js提交表单方法
form.submit()
```

可以通过js的submit（）方法来提交表单，不存在提交按钮不影响提交，但用该方法提交不产生sumbit事件，不能通过事件处理程序验证数据，所以应该在提交前先做数据验证。

表单提交的最大问题是有可能会提交两次表单。解决方法：1、在表单点击后禁用提交按钮，2、通过onsubmit事件处理程序取消后续的提交。

#### (2)重置表单

点击type属性为“reset”的<input>或<button>的重置按钮可重置表单。经过重置表单，表单字段会变为默认值或者空值（未设置时）。通过此方法重置表单会产生“reset”事件，可依照以上方法取消重置表单。

也可用用js的reset（）方法重置表单，与submit（）方法不同，经过JavaScript调用reset（）方法会触发reset事件。

#### (3)表单字段

 表单元素可以通过原生DOM方法进行访问。所有的表单元素都是表单elements属性（元素集合）中包含的一个值。elements集合是一个有序列表。包含表单中所有字段的引用。包括<input>、<textarea>、<button>、<select>和<fieldset>元素。按html页面的次序保存，可以通过索引值和name属性访问。

如果多个字段用了同一个name，则返回同名元素的htmlcollection。

##### 1)表单字段的公共属性

除<fieldset>元素外，所有表单字段都有一组同样的属性。

disable：布尔值，表示表单字段是否被禁用

form：指针，指向表单字段所属的表单，属性为只读。

name：字符串，这个字段的名字。

readOnly：布尔值，表示字段是否只读。

type：字符串，表示字段类型，如checkbox、radio等

value：要提交给服务器的字段值。对文件输入字段来说，这个属性是只读的，仅包含计算机上某个文件的路径。

除了form属性外，可通过js动态修改任何属性。

之前提到的防止多次提价表单，可以用修改表单字段的公共属性来实现：

```javascript
//假定现有id为‘myform’的表单，其提交按钮为id名mybtn的按钮
let form = getElementById('myform');
form.addeventlistener('submit',(event)=>{
    let target = event.target;
    //当表单内有多个submit时，用id寻找元素确保找到触发的字段
   	let btn = target.element['mybtn']；
    btn.disable = ture;
});
```

这个功能不能通过click事件进行处理，因为根据浏览器不同，点击按钮时，触发click和submit的次序也不同，但click在submit之前触发时，则首次的提交也没有生效。

type属性值：

| 描述             | 实例html                        | 类型的值          |
| ---------------- | ------------------------------- | ----------------- |
| 单选列表         | <select></select>               | 'select-one'      |
| 多选列表         | <select multiple></select>      | 'select-multiple' |
| 自定义按钮       | <button></button>               | 'submit'          |
| 自定义非提交按钮 | <button type='button'></button> | 'button'          |
| 自定义重置按钮   | <button type='reset'></button>  | 'reset'           |
| 自定义提交按钮   | <button type='submit'></button> | 'submit'          |

对于<input>和<button>，可以动态修改其type属性，但<select>上的type是只读的。

##### 2)表单字段的公共方法

每个表单字段有两个方法：focus（）和blur（）。focus（）将浏览器的焦点设置到表单字段上，意味着该字段可以响应键盘事件。

**在加载页面后将焦点定位在表单中的第一个字段是常见做法。**方法是在load事件添加事件处理程序并在第一个表单使用focus（）。如果第一个表单的第一个字段为type为‘hidden’的<input>元素，则代码出错。

html5对字段新增autofocus属性，自动为带有该属性的元素设置焦点。为了与js的focus（）方法兼容，先检测元素上是否有autofocus属性，若无再使用focus方法。

```javascript
//假定未知表单首个字段是否添加了autofocus，对原添加方式进行改进
window.addeventlistener('load',event=>{
    let element = document.form[0].element[0];
    //添加能力检测判断是否存在autofocus
    if(element.autofocus !== true){
        element.focus()
    }
})
```

blur（）方法为移除焦点，调用blur时，焦点不会转移，只是在对应字段移除了。

##### 3)表单字段的公共事件

blur：在字段失去焦点时触发

change：在<input>和<textarea>元素额定value发生变化且失去焦点时触发，或者在<select>元素中选中项发生变化时触发

focus：在字段获得焦点时触发

focus和blur事件通常以某种方式改变用户界面，已提供可见的提示或额外功能（如在文本框下边显示下拉菜单）。change事件通常用于验证用户在字段输入的内容。如：focus可以改变焦点背景颜色表示被选中，blur恢复颜色，change事件检测用户在输入了不合规值时显示警告。

```javascript
let textbox = document.form[0].element[0];
textbox.addeventlistener('focus',(event)=>{
    let target = event.target;
    if(target.style.backgroundcolor != 'red'){
        target.style.backgroundcolor ='yellow';
    } 
});
//在移除焦点和change时判断value是否为数值，
textbox.addeventlistener('blur',(event)=>{
    let target = event.target;
    // /[^\d]/匹配非数值，输入非数值返回true
    //三元运算符，true时返回red，false返回空白
    target.style.backgroundcolor =/[^\d]/.test(target.value)?'red':'';
    } 
});
textbox.addeventlistener('change',(event)=>{
    let target = event.target;
    target.style.backgroundcolor =/[^\d]/.test(target.value)?'red':'';
    } 
})
```

### 2、文本框编程

表示文本框有单行文本框<input type='text'/>（不设置type值直接显示文本框）和多行文本框<textarea></textarea>两种。

<input type='text'/>的size属性指定文本框的宽度（按字符计量），value属性指定文本的初始值，maxlength属性指定文本框允许的最多字符数。

\<textarea\>元素创建多行文本框，rows属性指定文本框的高度（按字符计量），cols属性指定文本框的宽度（按字符计量）。多行文本框的初始值在标签内部。

两种方法都可以通过value值访问内容。

#### (1)选择文本

支持





## 八、额外内容

### 1、正则表达式

正则表达式是一组判断对应字符串是否符合正则表达式定义的一种工具。在js编程中有字面量模式和字符串模式。

一般正则表达式以^匹配开头内容，以$匹配结尾内容。

### 2、三元运算符

形如 A ? B : C 的表达式为使用了三元运算符的判断语句。逻辑如下

```javascript
if( A ){
    B;
}else{
    C;
}
//即判断 A 的布尔值，true时执行B；false时执行C。
```



