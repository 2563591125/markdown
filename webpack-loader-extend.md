##### webpack的依赖图
- 事实上webpack在处理应用程序时，它会根据命令或者配置文件找到入口文件
- 从入口关系开始，就会生成一个依赖图关系，这个依赖图会包含应用程序中所需的所有模块（比如.js文件、css文件、图片、字体等）
- 然后遍历图结构，打包一个个模块（根据文件的不同使用不同的loader（装货的人、装货设备、装货机）来解析），打包好之后形成静态资产
##### import "./content/div_style.css"
- 如果一个模块只是做了一个引用，而这个模块你没有做任何的导出就可以直接import "./content/div_style.css"
- 但是如果没有loader，仍可以处理js文件，但是用import引入.css后缀的文件出现在webpack依赖图关系中时，就会报错
- 需要配置loader来解决import "...css"的问题
##### css-loader的使用
- loader可以用于对模块的源代码进行转换
- 我们可以将css文件也看成是一个模块，我们是通过import来加载这个模块的
- 在加载这个模块时，webpack（内置处理js功能，但有些其他功能没有内置，像是.vue等）其实并不知道如何对其进行加载，我们必须指定对应的loader来完成这个功能
  - 比如说vue开发.vue文件，webpack不知道怎么使用，vue-loader里面就会有一个配置文件来告诉webpack怎么使用。
  - 这个vue-loader的配置文件中的module：rules告诉webpack用这个vue-loader就能处理.vue
- webpack可以在原有的基础上扩展各种loader，这就是webpack的强大之处
- 处理.css文件最常用的css-loader
##### 配置css-loader
- module.rules中允许我们配置多个loader（因为我们也会使用其他的loader，来完成其他文件的加载）
- 这种方式可以更好地表示loader的配置，也方便后期的维护，同时也让你对各个loader有一个全局的概览
- 在webpack.config.js里面写
  module:{
    rules:[
        {
            //告诉webpack要匹配什么样的文件
            test:/\.css$/, //遇到这种文件
            use:[
                {
                    loader:"css-loader" //使用这
                }
            ]
        }
    ]
  }
  - rules是一个数组，数组里应该有很多对象，但这里因为只用到css-loader所以只遇到一个对象
  - 对象属性有text、use、loader等
  - use是一个数组，里面也有相应对象
- css-loader只负责解析.css文件，但不负责把css文件放到页面中，如果需要把css文件放到页面中我们需要另外一种loader，style-loader
##### style-loader
- 用之前需要先下载:npm install style-loader -D
- 已经可以通过css-loader来加载css文件了，但是发现css代码并没有生效
- 因为css-loader只负责将css文件进行解析，并不会将解析之后的css插入到页面中
- style-loader来实现这个功能
- 因为解析和插入是并列
  -  在webpack.config.js里面写
  module:{
    rules:[
        {
            //告诉webpack要匹配什么样的文件
            test:/\.css$/, //遇到这种文件
            use:[  //use中的loader使用顺序是从右往左，从下往上（从后往前），所以先使用style-loader
                {
                    loader:"style-loader" //使用这个
                }，
                {
                    loader:"css-loader" //使用这个
                }
            ]
        }
    ]
  }
##### less-loader
- npn install less-loader -D,注意：除了.js其他的loader都需要下载
- 在webpack.config.js里面写
  module:{
    rules:[
        {
            //告诉webpack要匹配什么样的文件
            test:/\.less$/, //遇到这种文件
            use:[  //use中的loader使用顺序是从右往左，从下往上（从后往前），所以先使用style-loader
                {
                    loader:"style-loader" //使用这个
                }，
                {
                    loader:"css-loader" //使用这个
                },
                {
                    loader:"less-loader" 
                }
            ]
        }
    ]
  }
##### PostCSS工具
- 什么是PostCSS
  - PostCSS是一个通过JavaScript来转换样式的工具
  - 这个工具可以帮助我们进行一些css的转换和适配，比如自动添加浏览器前缀、css的样式重置
  - 但是实现这些功能，我们需要借助PostCSS对应的插件
  - 在webpack.config.js里面写
  module:{
    rules:[
        {
            //告诉webpack要匹配什么样的文件
            test:/\.css$/, //遇到这种文件
            use:[  //use中的loader使用顺序是从右往左，从下往上（从后往前），所以先使用style-loader
                {
                    loader:"style-loader" //使用这个
                }，
                {
                    loader:"css-loader" //使用这个
                },
                {
                    loader:"PostCSS-loader"  //在解析css之前将css样式设定好
                }
            ]
        },
        {
            test:/\.less$/,
            use:[
                 {
                    loader:"style-loader" //使用这个
                }，
                {
                    loader:"css-loader" //使用这个
                },
                {
                    loader:"less-loader" 
                }
            ]
        }
    ]
  }
##### postcss插件 autoprefixer（很少用到）
- PostCSS是一个工具，药效添加前缀需要在下载扩展
- autoprefixer这个插件，所以需要:npm install autoprefixer -D
- module:{
  rules:[
    {
        test:"/\css$/",
        use:[
            {
                loader:"style-loader"
            },
            {
                loader:"css-loader"
            },
            {
                loader:"PostCSS-loader",
                options:{
                    postcssOptions:{
                        plugins:[
                            "autoprefixer"
                        ]
                        } 
                }
            }
        ]
    }
  ]
  }
- 因为这么些太麻烦了，所以我们用一个postcss.config.js的位置文件用来写这个
  - 里面写入，用PostCSS-loader之后，调用这个就可以加前缀了
  module.exports={
      plugins:[
         require("autoprefixer")
         ],
  }
  - module:{
  rules:[
    {
        test:"/\css$/",  
        use:[
            {
                loader:"style-loader"
            },
            {
                loader:"css-loader"
            },
            {
                loader:"PostCSS-loader",
            }
        ]
    }
  ]
  }
  - 经过写入之后，css文件会自动加浏览器前缀，但less不会，因为没有设置，如果需要的话要在/\.less$/后面加上
##### postcss-preser-env 插件 预设（提前将看到的插件内置进去）
- 事实上再配置post-loader时，不需要使用autoprefixer
- 我们可以使用另外一个插件：postcss-preset-env
  - 可以实现现代css特性，转成大多数浏览器认识的css
  - 事实上用这个就可以把autoprefixer内置进去
  -   module.exports={
      plugins:[
         require("procss-preset-env") //require目前可以无条件省略
         ],
  }
- #66666666 webpack不认识浏览器不识别，这就需要postcss-preser-env就可以将这个转化成webpack可打包浏览器可识别
##### webpack打包图片
- 每一个包都是一个模块，图片也可以是一个模块，所以可以用import aaa from "./img/aaa.img"引入图片
  - 可以在引入这个模块的时候给取个名字
  - 我们是通过import a from "./img/aa.png"来引入这个图片，然后通过const imgE1=document.createElement('img')来用这个推图片
- 我们用npx webpack打包，会报错，因为.png webpack也不识别，早期webpack用file-loader处理图片
- 现在图片不需要下载什么loader，但要告诉webpack怎么处理，所以在webpack.config.js里面写入：
  - module:{
  rules:[
    {
        test:"/\css$/",  
        use:[
            {
                loader:"style-loader"
            },
            {
                loader:"css-loader"
            },
            {
                loader:"PostCSS-loader",
            },
        ]
    }
    {
        test:/\.(png|jpe?g|svg|gif)$/,            
         //?表示0个或者1个，这里表示只要有这里面的一种就触发
        type:"asset",
    }
  ]
  }
- 在webpack5之前，加载这些资源我们需要使用一些loader，比如raw-loader、url-loader、file-loader;
- 在webpack5开始，我们可以直接使用资源模块类型（asset module type）,来替代上面这些loader;
- 所以现在已经不用下载loader了，只需要将type写入webpack.config.js
##### 认识asset module type
- 资源模块类型通过添加四种新的模块类型，来替换所有这些loader
  - asset/resourc  打包两张图片并且这两张图片有自己的地址，降低至设置到img/big中
  - asset/inline 
  - asset
- ***注意webpack.config.js必须有出口，不管webpack.config.js和index.js的名字对不对，都要module.exports{output}***
##### url-loader的limit效果
- 开发中我们往往是小的图片需要转换，但是大的图片直接使用图片
  - 这是因为小的图片转化内base64之后可以和页面一起被请求，减少请求过程
  - 大的图片也进行转换反而影响速度
- 我们需要两个步骤来实现
  - 将type修改为asset
  - 添加一个parser属性，并且指定dataUrl的条件，添加maxSize属性
##### 为什么需要babel
- 事实上，在开发过程中我们很少去直接接触babel，但是babel对于前端开发来说，目前是不可缺少的一部分：
  - 开发中想要使用ES6+的语法，想要使用TypeScript，开发react项目，都是离不开Babel的
  - 所以学习babel对于我们理解代码从编写到线上的转变过程至关重要
- 那么，babel到底是什么
  - babel是一个工具链，主要用于旧浏览器或者环境中将ECMAScript2015+的代码转换为向后兼容版本的JavaScript
  - 包括语法、源代码转化
##### babel-loader处理.js（webpack处理.js文件）
##### babel.config.js
- module.exports{
  plugins:[
    "@babel/plugin-transform-arrow-functions",
    "@babel/plugin-transform-block-scoping"
  ]
  }
##### 防止用到这么多插件，用babel预设preset
- npm install @babel/preset-env -D
- 有了预设就不用一个一个配置插件了，上面代码就要改了
- module.exports{
 presets:[
    "@babel/preset-env"
 ]
  ]
  }
###### babel常见的预设 env、react、TypeScript
##### webpack是如何查找和解析路径的
import utils from './utils/format.js'
- 如果是一个文件
  - 如果文件具有扩展名则直接打包
  - 否则将使用resolve.extionsions选项作为文件扩展名解析
- 如果是一个文件夹
  - 会在文件夹中根据resolve.mainFile配置选项中指定的文件顺序查找
  - resolve.mainFiles的默认值时['index']
  - 再根据resove.extensions来解析扩展名 
- extensions是解析到文件时自动添加扩展名:
  - 默认值时['.wasm','.mjs','.js','.json']（会根据自己的需求自己来配）;
  - 所以在import from需要调用的时候如果是.vue或者jsx或者ts文件时，我们必须加上扩展名
- 另一个好用的功能是配置别名alias
  - 特别是当我们项目的目录结构比较深的时候，或者一个文件的路径可能需要../../../这种路径片段
  - 我们可以给某些常见的路径起一个别名 
  一般这种./a/b/bb这种的没事，一般不喜欢../
- resolve:{
  extensions:[".js",".json",".vue",".jsx",".ts",".tsx",]
  },
  alias:{
    utils:path.resolve(_dirname,"./src/utils")
  }


***webpack插件、开启服务器用到的时候再回头看，还没有学完***