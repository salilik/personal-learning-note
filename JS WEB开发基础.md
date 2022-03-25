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
