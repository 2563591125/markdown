##### 全局安装指定版本：npm install webpack@3.6.0 -g
##### 命令查找流程
- 在当前文档下的终端输入一个命令，首先会查找当前文档下有没有这个工具
  - 比如说yarn --version     就会查看在当前目录下有没有包含yarn的包
  - 所有命令都符合在当前目录找不到直接去环境变量中查找，而不会去子目录中查找，但这里有个特殊的：webpack
##### npx ：原理十分简单，到node_module下面的.bin目录下找相关命令
- npx是npm5.2之后自带的一个命令
- 作用很多，常用来调用某个模块的命令
- npx是在npm安装好的时候就安装好了
- 作用是直接在node_module的目录的bin目录下查找相关的包
  - 如果找得到直接执行，如果找不到去环境变量中查找，但是我们想查看webpack的版本就得找到node_module下的webpack找到这个文件然后查看版本，npx就可以用来解决这个问题   
  - 比如顶层目录下npx wepack --version，npx就自动去找位置自动输出版本号
  - webpack --version的话就是先查看当前目录有没有该文件，没有的话就去环境变量中查找，但也会去webpack这个包中去查看，然后对比如果webpack这个局部包中有的话就显示这个局部包中的，没有的话采用环境变量中的
##### webpack打包
- 由于npm将npx已经集成到里面了，所以可以直接webpack就可以通过局部的webpack打包。但是以前的需要借助npx打包
- 所以现在webpack打包的方法：
  - 1.npx webpack 
  - 2.webpack 
  - 3.在package.json中的script:"aaa":"webpack"
  - 注意：在package.json中输入命令，优先在node_module中查找，而不是去环境变量：例如：在script：“aaa”：npx webpack;通过npm run aaa这个npx可以去掉，只输入webpack的话就不是从环境变量中查找了而是由先从node_module中查找
  - 即在package.json中的命令都首先从node_module中查找
##### 编写自己的工具/库/框架--->传给npm registry库--->张三下载 过程
- 先写js
- 初始化npm init
- 将当前的项目发布出去网页：
  - 注册npm账号 https://www.npmjs.com/ 
  - sign in
  - npm login登录
  - 修改package.json
  - npm publish 发布
    **发布时候遇到的问题**
    我的问题是：包名重复，所以需要重命名，也需要在package.json中修改name
    还有其他问题像是：npm registry设置为了淘宝镜像库需要修改回来
  - 重新建立一个文件/src/index.js
  - npm init
  - npm i/install mttt_first (开发和生产都依赖)
  - 在新的文件中写一个index.js 
  - 用webpack打包  下载npm webpack webpack-cli -D--打包 npx webpack
    ***webpack可以将你导入的也给你打包***
  - 然后再src中建立一个index.html 用script：src、type=module引入index.js
  - 用live server调试
    ***注意所有的路径必须正确***
    ***重新发布的话也要修改版本号***
  - 删除发布的仓库：npm unpublish
  - 让发布的仓库过期：npm deprecate
##### 再发布后引入之后做项目遇到的问题
- 1.在浏览器中运行必须用详细的路径，而node中可以写的随意点，因为会自动查找目录下的index.js
  - 因此需要webpack，这样浏览器也可以用只写目录的写法
- 2.在node中并不支持es6模块化的写法，也就是es module需要在packagejson中写入： test：module
##### 为什么使用pnpm
- npm在安装依赖时总是把包下载到磁盘中，当项目多时就会占用大量内存，pnpm就是来解决这个问题的
##### pnpm
- pnpm是performant npm高性能的npm
- 快速：比其他包管理工具快两倍
- 高效：node_modules中文文档链接自特定的内容寻址存储库
- 支持monorepos
- 严格 ...
- vue全面转向pnpm了
##### 软连接和硬链接
- 硬链接 hard link
  - 是电脑文件系统中的多个文件平等地共享同一个文件存储单元
  - 删除一个文件名字后，还可以用其他名字访问该文件
- 符号链接（软连接soft link、symbolic link） 
  - 包含一条以绝对路径或相对路径地形式指向其他文件或目录的内容
- <table>
  <tr>
  <td>存放路径，是个路径引用</td>
  <td>通过这连接到绝对路径这是软连接，相当于快捷方式</td>
  </tr>
  <tr>
  <td>D:\...位置</td>
  <td>可以是cba.mp4，通过这个来连接数据是硬链接</td>
  </tr>
  <tr>
  <td>数据data</td>
  <td>来存放文件数据</td>
  </tr>
  </table>
- 通过点击快捷方式连接到盘符里地文件这是软连接
- 通过点击盘符里文件连接到数据这是硬链接
- 这个数据可以是很多，可以有几个盘符里的文件指向同一个文件存储单元
##### 软连接和硬连接的演练
- 文件拷贝
  - window:copy foo.js foo_copy.js
  - macos:cp foo.js foo_copy.js
  - 文件的拷贝会在硬盘中复制出一份新的文件数据：复制出的文件相同、数据相同，新文件指向新数据，旧文件指向旧数据，但文件跟数据是相同的
- 文件的硬链接
  - 不能操作目录只能操作文件
  - 给bbb.js创建创建硬链接文件 mklink /H aaa.js bbb.js
  - 修改aaa.js，bbb.js里面的内容也会发生改变
  - 硬链接可以多个指向一个数据
- 文件软连接
  - mklink aaa.js bbb.js 创建符号软连接
- **注意：给a.js创建b.js硬链接需要固定格式，并且a.js是要存在的b.js不能存在的；但是给a.js创建b.js软连接，这俩都不能存在**
- **如果b.js时a.js的软连接的话，当链接地址为这个b.js软连接时，打开的是a.js，如果他俩是硬链接地址是谁就打开的谁**
##### pnpm做了什么事：
- ***通过pnpm add dayjs的方式下载dayjs库，并且把这个库的数据存到一个位置；如果做了多个项目，每个项目都要用到的话，只要往数据上建立硬链接就好；节省空间*** 
- 当使用npm或者yarn时，如果你有100个项目，并且所有项目都有一个相同的依赖包，那么，你在硬盘上就需要保存100份该相同依赖包需要的副本
- 使用pnpm，依赖包将被存放在一个统一的位置，因此
  - 如果对同一依赖包使用相同的版本，那么磁盘上只有这个依赖包的一份文件；
  - 如果对同一依赖包使用不同版本，则仅有版本不同的文件会被存储起来
  - 所有文件都保存在硬盘上的统一位置
  - 当安装软件包时，相关所有文件都会硬连接到这个位置不会占用硬盘空间
##### pnpm 创建非扁平的node_modules目录
- 当使用npm或yarn安装依赖包时，所有软件包都被提到node_modules下面，其结果是源码可以访问本不属于当前项目所设定的依赖包
- 使用过程
  - 所有工具包在使用之前都要创建 一般都会上传到npm的registry中npm install pnpm
  - 初始化 pnpm init 创建一个package.json，跟npm创建的没有区别
    pnpm初始化直接默认-y不用输入-y，直接进入修改就行
  - 在下载axios这个库的时候我们通过pnpm add axios（pnpm节省空间，并且非扁平）
  - axios有依赖一些其他包，但是我们用pnpm下载后node_modules里面没有
  - pnpm下载下来的axios是一个软连接，通过require获取axios应用，是根据软连接直接获取他硬盘路径的；而这个axios一共有两个文件夹，其中pnpm的就是存放软连接链接地址（真文件）的位置
- pnpm下载的库通过硬链接和软连接相互连接的方式，来最终实现，所以这成为非扁平
##### 目前前端开发流程
- 最流行：vue/react/angular

- 做项目先搭好结构：
  - 用什么包管理工具 npm/yarn
  - 用什么打包工具webpack
  - 用什么框架 vue/react/angular
  - 不用从0搭建，都有脚手架-cli；脚手架的目的是搭建基础- 结构；不管是vue还是react的脚手架都是基于webpack的，在每个脚手架都把webpack给搭建好了
  - 结构式：根目录下包含
    node_modules
    src：下编写源代码：index.js作为入口；app.vue（vue起的名字）在里面写html、css、js/app.jsx（react起的名字）里面也是写的html、css、js
    package.json
    babel.config.js....等等等等
   - npm/yarn：而在这个开发期间需要用到某个包就需要npm/yarn下载：像是axios、dayjs
- 浏览器不认识这些东西，但是为什么还用这个，因为比较好用，只要在我们做完之后在转换就可以；这个转化的过程就是打包，而打包的话就用到webpack，把每一个文件都转换成浏览器认识的东西（html+css+JavaScript（es5））
- 打包工具例如：guip、rollup、webpack、vite
  - 这些打包工具程序都是js代码，做一些文件操作
  - 运行的环境就是node环境即这些打包工具的运行依赖的时node环境，都跑在node环境上
- 从左向右看
  <table>
  <tr>
  <td>
  node_modules
    src：下编写源代码：index.js作为入口；app.vue（vue起的名字）在里面写html、css、js/app.jsx（react起的名字）里面也是写的html、css、js
    package.json
    babel.config.js....等等等等
  </td>
  <td>
  打包工具例如：guip、rollup、webpack、vite
  </td>
  <td>
  把每一个文件都转换成浏览器认识的东西（html+css+JavaScript（es5））
  </td>
  <td>
  静态服务器
  </td>
  <td>
  用户的浏览器
  </td>
  </tr>
  </table>
##### node中的内置模块path
- path模块用于对路径和文件进行处理，提供了很多好用的方法
- Mac OS、Linux和window上的路径是不一样的
  - window上回使用\或者\\，来作为文件路径分隔符当然也支持/
  - Mac OS、Linux的Unix操作系统上使用/来作为文件路径的分隔符
- 之后在不同系统上部署时其他系统不认识，但一个一个改太麻烦
- 解决：通过一个模块，用node根据不同操作系统给到不同的路径
- 可移植操作系统接口（英语：Portable Operating System Interface，缩写为POSIX）
  - linux和Mac OS都实现了POSIX接口
  - Window部分电脑实现了POSIX接口
##### path模块的使用
- path获取基本信息

```
const filepath =require('path')
console.log(path.extname(filepath))  获取文件后缀名
console.log(path.basename(filepath)) 返回文件的最后一部分  比如d：\\sss\a.txt 就反回a.txt
console.log(path.filename(filepath)) 获取当前文件的绝对路径，包含当前文件
```
- 拼接路径path.join
  - 希望将不同路径拼接，但不同路径用的不同的分割符 
- 拼接绝对路径 path.resolve
  - 从右往左依次解析path段，直至生成一个绝对路径，如果没有就跟当前目录拼接，0长度的会被忽略
  - 比如：
  console.log(path.resolve("./aaa","./bbb/aa","./abc"))
  如果 console.log(path.resolve("./aaa","./bbb/aa","/abc")) 就会生成/abc 因为/被看作根目录的意思（遇到绝对库路径就停止）
  如果 console.log(path.resolve("./aaa","/bbb/aa","./abc")) 就会生成/bbb/aa/abc  这个./相对路径是相对左边的路径来说的
  如果  console.log(path.resolve("/aaa","./bbb/aa","./abc")) 就会生成/aaa/bbb/aa/abc
  但是如果在所有path段中都没有绝对路径，就会跟当前目录拼接 d：//aaa/bbb/aa/abc
  如果 console.log(path.resolve("/aaa/cba","../bbb/aa","./abc")) 就会生成/aaa/bbb/aa/abc   没有cba，因为../往上反一层
##### webpack
- 三大框架的脚手架（cli）:vue-CLI、create-react-app、angular-CLI都是基于webpack来帮助我们支持模块化.
- webpack is a static module bundler（打包） for modern（现代的） JavaScript applications（应用程序）
   - 为什么是静态（static）：将代码打包成静态html+css+js 
   - 为什么是module bundler：因为webpack将CommonJS、es module、amd、cmd都给设置好了而且可以混合使用
   - 现代的modern：现代应用程序的复杂，促使webpack的出现和发展
- 作用:bundler your asset（资产、财富）
##### webpack具体功能
- JavaScript的打包
  - 将ES6转换成ES5的语法；   babel的作用，但webpack会将其集成在里面
  - Typescript的处理，将其转换成JavaScript；
- css的处理
  - css文件模块的加载、提取
  - less、sass等预处理器的处理
- 资源文件img、font
  - 图片img文件的加载
  - 字体font文件的加载
- HTML资源的处理
  - 打包HTML资源文件
- 处理vue项目的SFC文件.vue文件
##### webpack的使用前提
- 官方文档https://webpack.js.org/
  - webpack的中文官方文档时https://webpack.docschina.org/
- webpack的运行依赖node环境
  - 需要先安装node.js，会同时安装npm
##### webpack的安装
- webpack4开始安装需要安装两个：webpack、webpack-cli
  - webpack-cli是用来在命令行操作webpack
  - 如果只是在.js等文件中写不需要；但是webpack -entry只要是识别命令行就需要webpack-cli
- webpack和webpack-cli的关系
  - 执行webpack命令会找到node_modules下的.bin目录下的webpack
  - webpack在执行时是依赖webpack-cli的，没有安装就会报错
  - 而在webpack-cli在执行的时候才是真正利用webpack编译和打包的过程
  - 所以在安装webpack时，我们需要同时安装webpack-cli（实际上第三方的手脚架实际上没有用到webpack-cli的而是类似于自己的vue-service-cli的东西）
- npm install webpack webpack-cli -g#全局安装
- npm install webpack webpack-cli -D#局部安装
- 实际上局部安装比较好，因为电脑上如果项目多的话用到的webpack版本可能不一样的
##### webpack运行，基本打包
- 在打包的时候，如果src下的文件不是index.js 在打包的时候就会报错，所以需要在打包的时候更改入口：
  - 在src下建个配置文件webpack.config.js放在package.json的目录下（固定写法）(因为是跑在node环境下面的一般用的是module.exports而不是esmodule中的export )
  const path=require("path");
  module.exports={
    （入口）entry:"./src/main.js", //入口改为main.js
    （出口）output:{  //输出
      filename:"bundle.js",   //输出的名字
      path:path.resolve(__dirname,"./build")  //path：必须是绝对路径,将目录路径和./build拼接；意思是在build文件夹下生成bundle.js
    }
  }
  然后npx webpack打包就行了
- 需要注意的是webpack.config.js如果不是叫这个名字的话npx webpack打包找不到这个文件夹还是会出现main.js的错误
- 如果想避免这个错误 npx webpack --config wk.config.js（假如想用这个名字）
- 但是这样写命令太长了，我们可以把这条命令放到package.json的script中，用npm run build来执行
- 打包过程：
  - 第一步：npm init 创建package.json
  - 第二步：npm i webpack webpack-cli -D 安装局部的webpack 
  - 第三步：npx webpack 使用局部的webpack
  - 第四步：npm run build在package.json中创建scripts脚本，执行脚本打包即可
  - 在通常情况下打包很复杂，可以在根目录下创建webpack.config.js来做为webpack的配置文件
  - 指定配置文件名webpack.config.js npx webpack --config wk.config.js
