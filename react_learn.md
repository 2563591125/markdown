### 初读react文档收获
##### node.js下载
- node 中LTS稳定版（LTS是long term suport  term是指从一段时间到另一段时间）
- current 最新版本（current当前的目前的）
- 安装后：
  - 下载完毕通过git hub here查看：npm --version可以看npm版本
  - node --version看node的版本


##### markdown基本语法
- ‘- ’该符号表示●
- 在每个标签后面需要加空格，否则在github容易乱
- markdown大部分都支持结尾空一到两格来实现，由于在编辑器中有意无意使用空格，所以有个兼容性很好的办法（几乎每个markdown都支持）就是HTML的`<br>`语法
- ``反引号用来注释代码
####  `<script type="text/babel" src="..."></script>`
- type是DOMString类型的，而在JavaScript中DOMString就是String，代表的是utf-16字符串，代表的js中的普通字符
- 如果type不写的话，默认是JavaScript类型
- type和src都支持MIME类型
##### MIME全称是Multipurpose Internet Mail Extensions 多用途互联网邮件扩展
- Multipurpose是多功能的 
- Mail是邮件
- Extensions是扩展 扩展插件的意思
- MIME是用来描述消息内容类型的标准，用来表示文件、文档或字节流的性质和格式
- 浏览器通常使用MIME格式而不是扩展名
- 结构：type/subtype，type是类型、subtype是亚的意思，比如:  
    超文本标记语言文本.html:text/html、普通文件.txt:text/plain、RTF文本.rtf：application/rtf、GIF图形.gif：image/gif
- 两种主要的MIME类型扮演了主要角色：  
    text/plain表示文本文件的默认值  plain是平原、纯、平淡的意思
    application/octet-stream表示了其他所有文件的默认值，意思是未知的应用程序文件
   - 像是image表示图像文件、vedio是视频文件、audio是音频文件，application是一种二进制文件
   - application是应用、应用程序、申请的意思
   - oct-stream是一种文件类型
- 对大小写不敏感但传统都是小写
##### text/babel是react中jsx的一种写法也是jsx特有的一种语法，跟JavaScript不兼容，凡是用了jsx的地方都要加上text/babel。一共需要以内三个库react.js、react-dom.js和browser.min.js，都要首先加载（先写）
##### reactDOM和react的区别，reactDOM只做浏览器和DOM的操作，react做除了浏览器和DOM以外的其他操作。reactDOM是react的一部分
##### 在script中的crossorigin
- js中window.onerror来捕获js中的错误信息，当跨域资源出现错误时，onerror会上传script error，并不会指名具体问题，浏览器为了安全考虑会隐藏其他域下的错误问题，但onerror依然会上报，产生相应的日志文件。当加上crossorign后，就会指明错误的具体位置。
#####什么是npm，什么是npx，什么是node
- npm全称是node package manager，是一个NodeJs包管理和分发工具，也就是说，npm是用来管理软件包的使用：要使用npm需要下载node因为node内置了npm
- npx是npx的执行者，使用npx可以运行和执行软件包
- node是一个js运行环境，浏览器也是一个js运行环境，js脱离了浏览器试运行不了的，现在不仅浏览器能运行js node也能。
##### 用npx create-react-app my-app创建完成后，把src内容删掉，更改为自己需要的css和js文件，localhost：3000去调用端口号显示页面也可以直接npm start。
##### node的输入和输出
- 
