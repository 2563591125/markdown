##### 1. ES module
- es module是ecma2015也就是es6里面提出的规范
- 浏览器本身支持es module
##### 2. webpack模块化打包工具
- es module是通过export的方式导出，CommonJS是通过module.exports导出；但是借助于webpack可以用这两种方式的任意一种方式导出（甚至能混搭）
- 导出（不管是es module还是CommonJS）和导入都会被浏览器打包（一个整体）webpack解析成为普普通通的js文件（没有进行任何的模块化开发）；如果浏览器不支持es模块化，webpack打包出来的是普普通通的js文件可以运行在任何浏览器上；支持的话可以直接使用；
##### ES module
- JavaScript没有模块化一直是它的痛点，所以才会产生我们前面学习的社区规范：CommonJS、AMD、CMD等，所以在ECMA推出自己的模块化系统时，大家也是兴奋异常。
- ES module和CommonJS的模块化有一些不同之处
  - 一方面它使用了import和export关键词（注意是export不是exports）；
  - 另一方面它采用编译期的静态分析，并且也加入了动态引用的方式
- ES Module模块根据采用export和import关键字来实现模块化
  - export负责将模块内的内容导出
  - import负责从其他模块导入内容
- 采用ES Module将自动采用严格模式：use strict
  - 一般严格模式需要在前面加use strict，但是模块化的js默认前面加上了use strict
- 浏览器es module需要`<script type="module"></script>`这就对浏览器进行了模块化
- 注意在进行浏览器模块化的时候，type="module"会出现跨域的问题，有两种情况：
  - 如果只是学习的话，在vscode上测试需要下载live server
  - 还有一种是在做项目的时候，再学方法
- 通过export来导出的语法：export{name，age，sayhello}、export{标识符1，标识符2，标识符3}；禁止：export{name：“aaa”；也禁止name=“aaa”}
- import导入语法：import {name，age，sayhello} from "./aaa.js"//注意必须加后缀名，如果用webpack的时候你忘记加它会给你加上
- 注意事项：
  - 1.在浏览器中使用es module时，必须在文件后加上后缀名：import {name,age,sayHello} from "./app.js"
  - 2.在打开对应html时，如果使用了es module时不能用浏览器默认方式代开，因为：默认的打开方式是通过本地文件的方式打开的（file：//...）---会报错；而通过live server是开启一个本地服务的方式打开（127.0.0.1：....）；
  - 如果以本地的方式打开的话，会遇到一个CORS错误，因为JavaScript安全性需要；你需要一个服务器打开；因此需要通过live server扩展（小型实时服务器）来测试，项目的话需要做的
##### es module中esport关键字
- 1.导出方式1
  - export{name,age}
- 2.导出方式2
  - 注意：导出export和导入import的名称，name就是name要一样
  - 可以用as起个别名，export{name as fname,age,sayHello};import{fname,age,sayHello}
- 导出方式3
  - 在定义的时候就导出了export const name="james";导出函数时export function sayHello(){console.log(""sayHello)}
- 导出方式1
  - import {name,age,sayHello} from "./aaa.js" 
- 导出方式2
  - 导出方式也可以起别名：起别名可以防止命名冲突
  - 比如说，在导入时：export const name="james";导出时import {name ,age ,sayHello} from "./aaa.js"  const name="aaa";name冲突，就可以给import {name as fffname,age,sayHello} from "./aaa.js"
- 导出方式3
  - import * as foo from "./aaa.js"给导出的这个模块起个别名
  - 调用的时候就直接console.log(foo.name)
- **导出和导入最常见的方式是导出1，3和导入1，2**
##### export和import的结合使用，在有些开源框架中会见到的高级并且方便的用法
- 平时开发我们一般用的导入导出放法
```
aaa.js
export function foo(){
  return "aaa"
}
bbb.js
import {foo} from "./aaa.js"
import {ccc} from "./ccc.js"
console.log(foo();)
ccc.js
export fuction ccc(){
  return "sccc"
}
```
- 新的开发思想或者是开发方式
  - 入口文件index.js 
```
aaa.js
export function foo(){
  return "aaa"
}
bbb.js
import {foo,ccc} from "./index.js"
console.log(foo();)
ccc.js
export fuction ccc(){
  return "sccc"
}
index.js
import {foo} from "./aaa.js"
import {ccc} from "./ccc.js"
export{
  foo,
  ccc
}
```
- 但是会很麻烦，先在各个模块导出，在index.js导入在导出，因此会有优化，即import和export的结合使用：
  - 优化1：index.js 这个入口文件里面直接写  优化1注重阅读性
  export {foo} from "./aaa.js"
  export {ccc} from "./ccc.js"
  - 这个意思是：导入和导出
  - 优化2：    优化2注重简洁性
  export * from "./aaa.js"
  export * from "./ccc.js"
  - **因此有文档说名哪个模块有哪个函数的时候用简洁性强的语法，否则用阅读性强的语法**
##### default用法
- 在前面学习的都是有名字的导入（named exports）
  - 在导出export时指定了名字
  - 在导入import时需要知道具体的名字
- 还有一种导出叫做默认导出（default export）
  - 默认导出时不需要指定名字
  - 在导入时不需要{}并且可以自己用来指定名字
  - 也可以和CommonJS混合使用
- 默认导出的使用
  - aaa.js
  ```
  function aaa(){
    return "aaa";
  }
  //之前导出export {aaa} ;
  默认导出1
  export default aaa;
  默认导出2
  export default function(){
    return "new aaa";
  }
  ```
  - bbb.js
  ```
  //之前的导出import { aaa} from "./aaa.js"
  默认导出1
  import asc from "./aaa.js";
  asc();
  默认导出2

  ```
  - 一个模块只能有一个默认导出
##### import函数
- 导入声明只能放到顶层使用，不能放到逻辑中。原因：在执行代码之前先扫描找import，导入完成后执行代码，但是放在逻辑中不执行逻辑的代码就没法import就报错了
- 在条件成立的时候导入方法
  - 例如
  ```
  写法1
  const importPromise = import("./aaa.js")
  importPromise.then(res=>{
    console.log(res);
    //console.log(res.name)
    //console.log(res.age)等
  })
  写法2（真是开发一般写法）
  import("./aaa.js").then(res=>{
    console.log(res.name);
  }) 
  ```
  - 其中promise是一个承诺（可以是一个回调函数或者什么函数），import（）是导入函数，.then是在承诺完成后该执行的 res=>{} 是function(res)
- 导入时path值不能能拼接
- 导入时import不能放到逻辑中的原因：
  - 因为js引擎解析es module时必须知道它们的依赖关系
  - 由于这个时候js代码没有任何的运行，所以无法在进行类似于if判断中根据代码的执行情况
  - 拼接路径也不行“./aaa“+”.js“这种也是错误的
- 如果确实希望动态加载某一模块
  - 如果需要加载路径，这个时候我们需要使用import（）函数来动态加载；
  - import函数返回一个Promise，可以通过then获取结果
##### import.meta是一个在es11（2020）新增特性，包含了这个模块的信息，比如这个模块url
##### es module解析过程
  https://hacks.mozilla.org/2018/03/es.modules-a-cartoon-deep-dive/
- 阶段1：构建（construction），根据地址查找js文件，并且下载，将其解析成模块记录
  - script[type=module]解析（parse）{下载import ”./aaa.js“等}-->module record     
  - 每一个.js文件对应一个模块记录
  - module record的作用：main.js下载并解析成模块记录后，其他在想import的时候不用重新下载
- 阶段2 实例化（instantiation），对模块记录进行实例化并且分配内存空间，解析模块的导入导出语句，把模块指向对应的内存地址
  - <table>
    <tr>
    <td></td>
    <td>main.js</td>
    <td><---foo.js</td>
    </tr>
    <tr>
    <td>模块记录 module record</td>
    <td>import{} from "./foo.js"
    </td>
    <td>>export function(){...}
    export const name="foo"</td>
    </tr>
    <tr>
    <td>模块环境记录 module environment record</td>
    <td></td>
    <td>name=”“</td>
    </tr>
    </table>
  -有导出的话就生成一个模块环境记录 name=”“
- 阶段3运行（evaluation），运行代码计算值，并将值填充到内存地址中
  - <table>
    <tr>
    <td></td>
    <td>main.js</td>
    <td><---foo.js</td>
    </tr>
    <tr>
    <td>模块记录 module record</td>
    <td>import{} from "./foo.js"
    </td>
    <td>export function(){...}
    export const name="foo"</td>
    </tr>
    <tr>
    <td>模块环境记录 module environment record</td>
    <td>name="foo"</td>
    <td>name=”foo“</td> 
    </tr>
    </table>
  - 模块环境记录里面开辟的内存赋值name=”foo“ （可以拿到但不能修改）