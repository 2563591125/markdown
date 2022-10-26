##### Node.js是什么
- Node.js是一个基于chrome V8引擎的JavaScript运行时环境  
  Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine.
- 也就是说Node.js是基于V8来执行JavaScript的代码，但是不仅仅只有V8引擎
  - 我们知道V8可以嵌入到任何c++应用程序中，无论是Chrome还是Node.js（c++应用程序），事实上都是嵌入了V8引擎来执行JavaScript代码；
  - 但是在Chrome浏览器中，还需要解析渲染HTML、CSS等相关渲染引擎，另外还需要提供支持浏览器操作的API、浏览器自己的事件循环等
  - 另外在Node.js中我们也需要及逆行一些额外的操作，比如文件系统读/写、网络IO、加密、压缩解压文件等操作。
  - engine是引擎的意思，V8是chrome和node.js中JavaScript引擎
##### 浏览器（chrome）和Node.js架构区别
<table style="text-align:center">
<tr>
<td>html、css</td>
<td>JavaScript</td>
</tr>
<tr>
<td>blink</td>
<td>V8</td>
</tr>
<tr>
<td colspan=2>中间层</td>
</tr><tr>
<td colspan=2>操作系统</td>
</tr>
</table>
<table style="text-align:center">
<tr>
<td>JavaScript</td>
</tr>
<tr>
<td>V8</td>
</tr>
<tr>
<td >中间层（libuv）</td>
</tr>
<tr>
<td >操作系统</td>
</tr>
</table>
 
- node有js代码，但是v8是c++的，但像是libuv就是用c语言写的，所以node由js、c、c++写的，也可能有其他语言，可能会不止一种语言
##### Node.js的应用场景
- 应用1：目前前端开发的库都是以node包的形式进行管理
- 应用2：npm、yarn、pnpm工具成为前端开发使用最多的工具
  - 这是两步但是同一个东西，把原来的库打包成node形式，然后用node管理工具：npm等下载
- 应用3：越来越多的公司使用node.js作为web服务器开发、中间件、代理服务器
- 应用四：大量项目需要借助Node.js完成前后端渲染的同构应用；
- 应用四：自身前端工程师需要为项目编写脚本（用js）
- 应用五：eletron用来开发桌面程序（离不开node）
##### Node的安装
- Node最早诞生在2009年，目前最新的版本是分别是LTS16.15.1以及Current 18.4.0;
- LTS版本（longterm support，长期支持），相对稳定，推荐线上环境使用该版本；
- Current版本：最新node版本，包含很多新特性
- node --version查看node版本
- npm --version查看npm版本
- windows想进入一个盘先用C：切换盘符
- 可cd进入在.js的盘符，通过node app.js调用js就可以不用在浏览器上显示
##### ~在安装node测试中用到了vim语句，vim的话是编写，进入vim后先i改为可写模式，写完esc切换到命令模式然后：①：wq表示保存退出②：wq！强制保存并退出③：q表示退出④：q！强制不保存退出~
##### Node的版本工具 
- n/nvm（不支持windows系统）版本工具可以有的作用：可以用来管理不同版本的node
  - nvm：Node Version Manager
  - n：Interactively Manage Your Node.js Version（交互式管理你的Node.js版本）
- 有开发出的nvm对应的windows的版本（可以从网上找到),n在windows上用不了
- nvm相关语句：①nvm --version 查看nvm版本 ②nvm list 查看nvm帮你管理什么版本的node③安装某个node版本nvm install 版本号；最新的nvm install latest④nvm use+版本号 切换版本（用管理员身份，要不没有权限）
- n还没看，等用mac在学 
- 想停掉一个命令时ctrl+c
##### 学会使用vscode自带的终端
##### javaScript代码执行
- 如果我们编写一个js文件,里面存放JavaScript代码,如何来执行它呢? 两种方式:
  - 将代码交给浏览器执行
  - 将代码放到node环境中执行
- 把代码交给浏览器执行:
  - 需要让浏览器加载解析html代码
  - 在html中通过script标签引入js文件l
  - 当浏览器遇到script标签是就会根据src加载,执行JavaScript代码
- 把js文件交给node执行
  - 首先在电脑上安装Node.js环境,安装过程自动配置环境变量
  - 可通过终端命令node.js文件的方式来再如何执行相应的js文件;
##### Node程序传递参数
- 正常情况下执行一个node程序,直接跟上我们对应的文件即可
  - node index.js
- 某些情况下传递参数node.js menvdevelopment coderwhy
  -  // 输入方式
  // process（进程）是全局关系
  // argv arg是argument是论点/论据/争论的意思 v是vector（容器）
  // 注意这里的[0],[1]是console.log(process.argv)显示的C:\Program Files\nodejs\node.exe D:\vscode web\js初步\a.js,所以要从2开始
  // 输入的书写方法就是node a.js 20 20(node.js之后每写一个输入就加个空格)
 `` const arg1 = process.argv[2];
  const arg2 = process.argv[3];
  console.log(arg1, arg2);``
  - 解释:获取process中的参数;
  - 找到argv属性,会发现一个数组里面包含了所需要的参数.
##### Repl
- node提供的类似于chrome浏览器临时编辑代码的那个环境就是Repl
- repl是read-eval-print loop的简称,翻译为:读取-求值-输出-循环
- repl是一个简单的,交互式的编程环境
- 在vscode终端直接输入node,想退出的话按两次crtl+c
- 在cmd终端中想清空用cls
- 真实开发一般不用
##### const和var
- const定义变量不可修改
- var 可提权；省略var定义的变量是全局变量
##### 全局变量
- node中没有Window，在node中使用全局变量是global,在window中的变量在node里放到global中
- global object称为全局对象
##### 特殊的全局对象
- 这些全局对象实际上是模块中的变量，不过每个模块都有，看起来像全局变量
- 在命令交互中是不可使用的
- 包括：_dirname、_filename、exports、module、require()
- 全局对象：
  - console.log(__dirname);打印目录结构（重要，用来当相对路径的时候打印相对路
  - console.log(__filename);打印目录结构加上文件名
  - console.log(process)一般用的比较多process.argv
##### node中的定时器  
- setTimeout、setInterval
- 立即执行函数setImmediate所以没不用加时间（，3000）
- 额外执行函数process.nextTick（（）=>{}），在下次 Tick中执行
##### global对象
- 在window（浏览器）中var a=“abc”；var定义的值是会传到window对象中；global中的var定义传到global对象中
- 在浏览器和node中都有globalThis（记两个名字容易搞混，新得ECMA标准）无论是window还是node都是全局对象，
##### global和window的区别
- 在浏览器中，全局变量都是window上的，比如document、setInterval、setTimeout、alert、console等；
##### 什么是模块化
- 事实上模块化开发最终目的是将程序划分为互不影响的结构（有的引入不同文件是可以相互影响的，所以不是在不同文件里就是模块化）
- 在这个结构中编写自己代码在自己的作用域，不会影响其它结构
- 这个结构可以将自己希望包括v的变量函数导出（export{name，foo}）给其他结构使用
- 也可以通过某种方式（import {name，foo} from “a.js”）导入其他的变量、函数、对象等
##### JavaScript的模块化（核心：导出和导入）开发
- JavaScript曾经缺陷‘；比如var定义的变量作用域问题
- 没法像常规的面向对象语言一样使用class
- 比如JavaScript没有模块化问题（早期）
- 如果直接script+src引入script，那引入的.js依然处于全局变量
- var name=“bbb”;
    console.log(name);
- let name=“bbb“ let不能重新命名，不会冲突，但仍然不能用name，因为已经被定义过（不同文件命名冲突）
    - 解决方法：function(){}()} 立即执行函数根据本身函数自带作用域的特点，给外界强势加了一个作用域，但由于有作用域其他函数没法获取需要在函数中return 想要给其他函数调用的值
    - 
- 模块化规范ECMAScript（没有模块化的时候）：CommonJs社区流行，而以前也流行过的AMD和CMD已经被淘汰了
- ES6（ES2015）推出自己的模块化方案
- 模块化历史：
  - ajax的出现，前后端实现分离，意味着后端返回数据后，用js对前端页面渲染
  - spa的出现，前端页面变得更加复杂：包括前端路由、状态管理等一系列复杂需求通过js来实现
  - 包括Node的实现，JavaScript编写复杂后端程序，没有模块化是致命伤（ES6(2015)，因为ECMA自己推出所以很多社区流行过时，但CommonJs依然流行）
##### 模块化过程
- 没有模块化带来许多问题：比如命名冲突
- 解决命名冲突：立即函数调用表达式
- 新问题：记住命名、代码混乱
- 解决新问题：
##### CommonJS（平时也会称CJS）规范和node关系
- Node是CommonJS在服务器端一个代表性的实现
- Browserify（现在已经不用这个了）是CommonJS中一种实现
- webpack打包工具具备对CommonJS的支持和转换
- CommonJS规范
  - `let name='why' function foo(){exports.name;}`
  - `const aaa=require("./a.js")    aaa.name`
  - 浏览器没有实现CommonJS
- node默认每个单独的文件也是一个模块；通过script+src写入html中浏览器，每个文件单独写完放到同一个html之后可以理解为一个整体，就不算模块，相同的名称如果没有作用域就会影响
- node因为不同文件是不同模块的原因，所以要用exports、require导出导入
 <table>
  <tr>
  <td>app.js</td>
  <td>aaa.js</td>
  <td>node aaa.js</td>
  </tr>
  <tr>
  <td width=400px>
let oname = "wwwwww";
function fa() {
    return "aaa";
}exports.oname = oname;
exports.fa = fa;
</td >
<td width=400px> 
const a = require("./app");
console.log(a);
console.log(a.fa());
</td>
  <td width=400px>
PS D:\vscode web\练习> node aaa.js
{ oname: 'wwwwww', fa: [Function: fa] }  aaa
</td>
  </tr>
  </table>

- 在拿到对象之后对其进行解构  解构后用的更简单 
  - 开始 `const a=require("./app") console.log(a.fa())`
  - 解构后`const {oname , fa()} console.log(fa()) console.log(oname)` 
- 导出和导入是模块化的核心
  - exports和module.exports可以负责对模块中内容进行导出
  - require函数可以帮助我们导入其他模块（自定义模块、系统模块、第三方模块中的内容）
- main.js
  - `let name="james"; console.log(exports.name); setTimeout(()=>{console.log(exports.name)}，4000)`
- another.js
  - `var bar =require("./main.js") console.log(bar.name);setTimeout(()=>{bar.name="kobe"}，2000)`
- 以上两个为node main.js的结果为exports.name位kobe，说明当两个导入导出属性后，用的是同一个属性，不管是谁改变都影响另一方的输出。实际上：bar变量就是exports对象了
##### module.exports导出
- 导入导出实际上：exports=0x1000   const bar=0x1000拿到导出的地址  实质上是三个指向相同的地址
- exports.name=name；这种给exports赋值的过程在开发中用的很少
- 如果用module.exports.name=name的化导出的效果跟上面其实是一个样的
- 开发中常见写法 module.exports={name，age，sayhello}//一旦写大框就是创建新对象，所以require就指向这个对象，因此这时候require改变属性值是不会改变对象中的值（当用exports、require的时候是他们同时拥有一个地址指向一个对象，所以改一个都改；而module.exports创建对象是module.exports对象，改变require不能修改对象里的值，所以里面不发生变化）
- 如果module.exports不创建对象的时候和exports、require三者指向相同，修改一个都发生改变（这实际上是一种不规范的做法，最好不要用一个导入者修改对象中的内容）
##### require细节
- const bar=require("./utils")可以省略index.js也可以写为const bar=require("./utils/index")省略.js
- 导入模块：
  - 根据路径导入自己编写的模块
  - 导入node提供的内置模块const bar=require(path/http/)
  - 查找：
    - 第一步：1.当x当作一个文件在对应目录下查找：如果有后缀名按照后缀名的格式查找对应的文件2.如果没有后缀名，会按照如下顺序：①直接查找文件x②查找x.js文件③查找x.json文件④查找x.node文件
    - 第二步：查找目录下的index文件①查找x/index文件②查找x/index.json文件③查找index.node文件
    - 找了很多找不到报错
  - 导入没有的东西const bar=require("wwsd ")，如果某个文件夹有这个字符，就自动查找这个文件夹下的/index.js
  - 导入没有的东西，并且x不是核心模块，会逐层网上查找，直到找到根目录下的nodemodule，如果还没有就报错
##### node模块的加载过程
- require导入的时候会先将需要导入的运行一次
- 但也只运行一次内部会缓存，下面再用require导入的时候不会在执行了
  - 内部会将每个模块抽象成为一个module对象，有个module.loaded属性，默认是module.loaded=false的当导入一次后，回想false改为true，下次再导入的时候内部代码就不会执行了
- 如果循环引入加载顺序是：深度优先算法
  - 先从一层走到底（树结构），aaa可以指向bbb、ccc，但是走到bbb的时候bbb需要走向ddd-->eee等这条线走完后再往回慢慢返回就是深度优先
  - 与其对立的是广度优先
##### CommonJS规范的缺陷
- CommonJS加载模块是同步的
  - 同步意味着只有等到对应的模块加载完毕，当前模块中的内容才能被运行
  - 在服务器不会有什么问题，因为服务器加载的js都是本地文件，加载速度非常快
- 如果应用于浏览器
  - 浏览器加载js文件需要先从服务器下载下来，在加载运行
  - 同步就意味着后续js都无法运行
- 因此在浏览器中一般不适用CommonJS规范
  - 但是webpack可以将多个js打包成一个下载一个就够，如果想分包也可以实现，这是后续
- 在早期为了可以在浏览器中使用模块化，通畅使用AMD或CMD
  - 但是目前一方面现代的浏览器已经支持ES Modules,另一方面借助于webpack可以实现对ES module或CommonJS的代码转换
  - AMD、CMD已经要被淘汰了