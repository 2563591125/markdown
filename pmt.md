##### 代码共享方案
- 1.官网发布
  - 手动下载、管理、删除相关依赖，版本更替的时候需要重复
- 2.github
  - 手动下载、管理、删除相关依赖，版本更替的时候需要重复
- 3.npm registry库 npm下载、上传
  - 通过代码发布特定的位置
  - 其他程序员通过工具安装升级删除我们的工具代码
##### 包管理工具npm
- Node package Manager，也就是node包管理
- 但是目前已经不仅仅是node包管理器了，在前端项目中我们也在使用它来管理依赖的包
- 比如vue、react、webpack等等等
- 如何让下载安装npm：下载node，自带npm
- 如何查看一个包在不在npm库里下载：
  - 查看官网、github
  -  查看安装相关的npm包的官网：npmjs.org（https://www.npmjs.org/、https://www.npmjs.com/）
##### npm配置文件package.json
- 用来记录 name、version、dependences:{}等
  ```
  {
    "name":"";
    "version":"1.0.2";
    "denpendences":{};
  }
  ``` 
- npm怎么来管理那么多包呢？
  - 无论前端项目（vue、react），还是后端项目（node）；
  - 这个配置文件会记录你的项目名称、版本号、项目描述等；
  - 也会记载着你项目所依赖的其他库的信息和依赖库（比如依赖dayjs、vue的库的等）的版本号
- 怎么得到这个文件：我们可以手动创建package.json但是开发中有两种方式：
  - 1.npm init 初始化文件 +回车*n
  - npm init -y 初始化文件 默认全部yes
  - 2.从0开发项目的时候要用上面的，不是从0开始的就会生成package.json，像是vue clj通过脚手架创建项目
##### 常见的配置信息
- 必须填写字段name、version
- 很重要字段，防止被发布private：true是不可发布
- main字段：
  - 设置程序入口
  - 比如使用axios模块    const axios=require("axios");
  - 如果有main属性，实际上是找到对应的程序入口文件的  main："main.js"  如果./axios就不是默认找index.js了而是找main.js了。如果是main：index.js这也是默认的
- scripts字段
  - "scripts":{"start":"node ./src/main.js"}，执行脚本的命令npm run start 运行start脚本；
  - 在开发中最常见的build和start，build一般用来打包
  - 对于特定名称的脚本通过npm start可以运行，其他的必须用npm run 
  - 允许特定名称的脚本 start、text、stop、restart可以省略掉run
- dependences依赖
  - 当给同事传项目快的时候，可以查看dependences依赖的库
  - 可以通过npm install dayjs vue这种方式下载，也可以直接npm install就可以把dependences里面的全部下载了
- devDependencies属性
  - 一些包在生成环境是不需要的，比如webpack、babel等
  - 这个时候我们会通过npm install webpack --save-dev，将他安装到devDependencies属性中
  - 生产（production）依赖：
  - 开发（development）依赖：开发环境依赖的（webpack打包、babel es6转es5）
  - 像是babel安装要npm install babel --save-dev，不然的话会安装到dependences中，不可以   可以save-dev用D代替
  - 只有开发和生产都依赖的才放到dependences里
- peerDependencies属性
  - 对等依赖
  - 做项目依赖一个库a这个库又依赖另一个库b，所以在下载库a之后打开package.json看peerDependencies就会看到b
  - 
##### 依赖的版本管理
- npm的包通常需要遵从semver版本规范
  - semver：https://semver.org/lang/zh-CN/
  - npm semver: https://docs.npmjs.com/misc/semver
- semver版本规范X.Y.Z;
  - X主版本号（major）:当你做了不兼容的API修改（可能不兼容之前的版本）；
  - Y次版本号（minor）：当你做了向下兼容的功能性新增（新功能增加，但是兼容之前的版本）
  - Z修订号（patch）：当你做了向下兼容的问题修正（没有新功能，修复了之前版本的bug）
- ^和~的区别
  - x.y.z：表示一个明确的版本号（写死了）
  - ^x.y.z：表示x是保持不变的，y和z永远安装最新的版本（灵活）
  - ~x.y.z：表示x和y保持不变的，z永远安装最新的版本（灵活）
##### npm install命令
- 局部安装（local install）npm install webpack   在哪个文件夹下就在哪里建立      一般局部安装都是安装某个需要的库
- 全局安装（global install）npm install webpack -g    注意：一般全局安装都是工具包
- 只要把对应的东西放到环境变量里面，可以用代码去取 比如：在命令行直接输入webpack没什么用，但是：先下载；后安装到环境变量；
  - 通过npm下载（本质是放node_module中，这样永远不会转到环境变量中），但是npm install webpack -g后就会将webpack安装到一个专门的目录，那个目录（node自己管理的）就是在环境变量里
- 项目安装
  - 项目安装会在当前目录下生成一个node_modules文件夹，我们之前讲的require查找顺序时，有讲过这个包在什么情况下被查找
  - 局部安装又分成开发时依赖和生产依赖
  - 默认安装开发和生产依赖  npm install axiox /npm i  axios
  - 开发依赖：npm install webpack --save-dev
    npm install webpack -D
    npm i webpack -D
  - 根据package-json中的依赖包
    npm install
##### npm install 原理
- npm install axios 去 registry中有没有包，有的话就下载下来。当这个包依赖其他包时，再去执行相同过程去下载其他包
- npm缓存（catch）
  - 当电脑有两个项目用到同一个包，去远程服务器下载两遍太浪费，这就涉及到一个缓存。   第一个包下载后，有缓存，第二个项目只要解压就行。
  - 缓存：得有个标识符；只有第二个项目找不到这个标识符，也就是找不到这个项目的时候，就需要重新下载
  - 存储这个标识符的文件：package-lock.json
  - package-lock.json将版本固定，防止多人工作的时候，共享过程中版本混乱问题（因为用dependencies  用npm install  下载的时候版本已经更新了，两个人用的不一样，然后共享返回的时候容易因为版本不同差生问题）
  - dependencies和require（早期）都可以来记录依赖的库  格式可能会有点差异，但是意思相同
##### npm其他命令   npm命令：https://docs.npmjs.com/cli-documentation/cli
- 卸载某个依赖包
  - npm uninstall package
  - npm uninstall package --save-dev //卸载开发依赖包
  - npm uninstall package -D  //卸载开发依赖包
- 强制重新build
  - npm rebuild
- 清除缓存
  - npm cache clean
- 获取缓存
  - npm config get cache 
##### yarn
- 原因
  - 早期的npm没有缓存，所以会下载很多分同一种包，安装速度慢、版本依赖混乱
  - npm5版本开始，进行了很多升级和改进，依然有很多人喜欢使用yarn
  - yarn有facebook、google等 联合推出
- yarn的使用
  - yarn也是分两步：安装、放到环境变量
  - 安装可用npm安装，因为npm有yarn这个包，因为yarn是个工具包，所以全局安装  npm install yarn -g
- yarn用法
  - yarn install 安装依赖 ，但是在有package.json的情况下，可以直接写yarn也会下载依赖   但是如果指明下载那个依赖 就要 yarn add dayjs
  - yarn init 初始化，下载package.json
  - yarn add axios dayjs   npm install ...
    yarn add dayjs -D/--save -dev
  - yarn run start 运行scripts
- yarn跟npm的差异：
  - yarn add axios dayjs/ npm install ...
    yarn add dayjs -D/--save -dev
  - yarn install --force（强制）   强制重新安装依赖
    npm rebuild
  - 删除 npm uninstall [package]
    yarn remove [package]
    npm uninstall -save [package]（安装的依赖包可保存在package.json中）
    npm uninstall --save -dev[package]
    npm uninstall --save -optional[package]
    **yarn remove [package]**
  - 升级
   npm：rm -f node_module&&npm install
   yarn upgrade
  - 清除缓存
  npm cache clean/yarn cache clean  
##### cnpm工具
- 由于一些特殊原因，某些情况下我们没法很好的从https://registry.npmjs.org下载下来（因为registry是国外库）
- registry 注册表、登记处，注册 登记
- 有时候npm下载不下来可能跟github一个原理
- 有时候很需要，但是连不进去就可以通过淘宝的镜像服务器仓库
  - 每过十分钟就从registry在镜像服务器里备份一份
  - 需要先将registry的仓库改为镜像服务器（从网上找代码，安装过程）
- 查看npm镜像  npm config get registry
- 直接设置npm镜像：npm config set registry https://registry.npm.taobao.org
- 修改npm镜像患处
  - 修改了从官方下载下来的包的渠道
  - 某天淘宝不运营了不维护了挂了  还要改
- 下载安装npm install cnpm -g
- 在安装cnpm的时候就更改registry库
  npm install -g cnpm --registry=http://registry.npm.taobao.org
- 安装完成的时候修改registry库 
  cnpm config set registry=https://registry.npm.taobao.org
- 查看 cnpm config get registry