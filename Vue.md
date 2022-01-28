---
title: Vue
date: 2021-10-08 9:48:05
tags: Vue
categories: 面试
cover: https://z3.ax1x.com/2021/10/27/5ToA10.png
---

# git

## 工作流程

1）在工作目录中修改某些文件

2）对修改后的文件进行快照，然后保存到暂存区域

3）提交更新，将保存在暂存区域的文件快照永久转储到Git目录中

## fetch、merge、pull

git pull相当于git fetch 和git merge，即更新远程仓库的代码到本地仓库，然后将内容合并到当前分支

- git fetch：相当于是从远程获取最新版本到本地，不会自动merge
- git merge：将内容合并到当前分支
- git pull：相当于是从远程获取最新版本并merge到本地

## git常用命令

```json
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/GWL0927/Notes.git
git push -u origin master
```

```json
1）从远程库中克隆项目
git clone 项目地址

2）工作区到暂存区
git add 文件名字、git add . 多个文件操作

3）暂存区到版本区
git commit -m"注释信息"

4）把版本区文件上传到远程仓库
git push origin master

5）将远程仓库的文件拉取/下载下来
git pull origin master

6）查看当前历史记录、查看所有的操作记录
git log、git reflog

7）查看文件状态
git status

8）查看版本信息
git version

9）查看配置信息
git config --list

10）在当前目录新建一个Git代码库（生成隐藏.git文件）
git init

11）版本回退
git reset --hard 版本id

12）查看xx文件修改了哪些内容
git diff xx

13）删除文件名
git rm 文件名

14）恢复一个文件
git checkout

15）关联一个远程库
git remote add [远程仓库git地址]

16）移除关联一个远程库
git remote remove [远程仓库git地址]

17）生成一个可供发布的压缩包
git archive
```



## **分支的相关命令**　

- 创建分支：git branch 分支名
- 查看分支：git branch
- 切换分支：git checkout 分支名
- 创建并切换分支：git checkout -b 分支名
- 合并分支：git merge
- 查看已经合并的分支/未合并的分支：git branch --merge / git branch --no-merge
- 删除的已合并的分支/未合并的分支：git branch -d 分支名 / git branch -D 分支名



# 前后端分离

在前后端分离的应用模式中，**后端仅返回前端所需的数据**，不再渲染HTML页面，不再控制前端的效果。但无论哪种前端，所需的数据基本相同，后端仅需开发一套逻辑对外提供数据即可。

![img](https://img2018.cnblogs.com/blog/1513642/201903/1513642-20190318170004467-1243010027.png)

## 前后端不分离

**前端页面看到的效果都是由后端控制**，由后端渲染页面或重定向，也就是后端需要控制前端的展示，前端与后端的耦合度很高。

这种应用模式比较适合纯网页应用，但是当后端对接App时，**App可能并不需要后端返回一个HTML网页，而仅仅是数据本身**，所以后端原本返回网页的接口不再适用于前端App应用，为了对接App后端还需再开发一套接口。

![img](https://img2018.cnblogs.com/blog/1513642/201903/1513642-20190318165752061-674910431.png)

## RESTful

RESTful是一种定义Web API接口的设计风格，尤其适用于前后端分离的应用模式中。

这种风格的理念认为**后端开发任务就是提供数据的**，对外提供的是数据资源的访问接口，所以在定义接口时，客户端访问的URL路径就表示这种要操作的数据资源。

1. **域名**

应该尽量将API部署在专用域名之下。

`https://api.example.com`

如果确定API很简单，不会有进一步扩展，可以考虑放在主域名下。

`https://example.org/api/`

2. **版本（Versioning）**

应该将API的版本号放入URL。

`http://www.example.com/app/1.0/foo`

`http://www.example.com/app/1.1/foo`

`http://www.example.com/app/2.0/foo`

3. **HTTP动词**

对于资源的具体操作类型，由HTTP动词表示。

常用的HTTP动词有下面四个（括号里是对应的SQL命令）。

- GET（SELECT）：从服务器取出资源（一项或多项）。
- POST（CREATE）：在服务器新建一个资源。
- PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
- DELETE（DELETE）：从服务器删除资源。

下面是一些例子。

- GET /zoos：列出所有动物园
- POST /zoos：新建一个动物园（上传文件）
- GET /zoos/ID：获取某个指定动物园的信息
- PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
- PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
- DELETE /zoos/ID：删除某个动物园
- GET /zoos/ID/animals：列出某个指定动物园的所有动物
- DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物

# 项目中的Element

## 不同类型信息的切换 el-tabs

[![5Ot029.png](https://z3.ax1x.com/2021/10/28/5Ot029.png)](https://imgtu.com/i/5Ot029)

## 信息展示el-table

[![5OtsDx.png](https://z3.ax1x.com/2021/10/28/5OtsDx.png)](https://imgtu.com/i/5OtsDx)

## 时间选择器el-date-picker

[![5OtgUO.png](https://z3.ax1x.com/2021/10/28/5OtgUO.png)](https://imgtu.com/i/5OtgUO)

## 分页el-pagination

[![IGOSw4.png](https://z3.ax1x.com/2021/11/08/IGOSw4.png)](https://imgtu.com/i/IGOSw4)

```json
queryParams: {
    pageNum: 1,
    pageSize: 12,
    designName: ''
} // 查询参数
```

项目中是后端分页：需要我们把页码、请求条数发送给后端，后端根据条件每次返回对应的条数。

# 项目难点

新增专家的时候，弹出表单，其中专家的工作经历、教育背景和所获荣誉数量不确定，然后我想达到的效果是，默认不显示这三类信息的输入框，分别显示三个新增按钮，点击就新增一类信息的输入模块。

解决：给每类信息模块外套一个div，workcount默认为零

[![5Otf8H.png](https://z3.ax1x.com/2021/10/28/5Otf8H.png)](https://imgtu.com/i/5Otf8H)

点击一次新增按钮，workcount+1，则就渲染一个信息模块

[![5OtOPg.png](https://z3.ax1x.com/2021/10/28/5OtOPg.png)](https://imgtu.com/i/5OtOPg)

# 路由懒加载

把不同路由对应的组件分割成不同的代码块

然后**当路由被访问的时候才加载对应组件**

[![5ONSrq.png](https://z3.ax1x.com/2021/10/28/5ONSrq.png)](https://imgtu.com/i/5ONSrq)

不采用路由懒加载则是，在最开始就加载了所有的组件，而不是在每个路由里要用的时候才加载。

# 后端一次性返回所有数据

## 前端分页

请求接口接收数据，一次性获取所有数据`this.allList`，展示列表数据`this.dataList`

当页码改变

```js
current_change(num) { // 当前页
    this.pagenum = num;
    this.datalist = this.allList.slice(
        (this.pagenum - 1) * this.pageSize,
        this.pagenum * this.pageSize
  );
}
```

当每页数量改变时

```js
size_change(size) { // 每页条数
    this.pageSize = size;
    this.datalist = this.allList.slice(
        (this.pagenum - 1) * this.pageSize,
        this.pagenum * this.pageSize
    );
},
```

# 项目中的axios

在创建的axios实例中，配置了baseURL，表示请求URL公共的部分

在request拦截器中，让每个请求携带token

为什么要携带token？

1、前后端分离的项目中，前端需要通过发送请求获取数据，为了安全，需要保证前端发送过来的请求有获取数据的权限

2、在需要登录的项目中，每次请求都需要为请求头添加token字段，表示自己已经登陆过，拥有权限

3、每次发送请求的时候就需要在请求中加入token字段

response拦截器：所有需要登陆的页面都需要加一个判断，用户token过期了，或者是伪造的，就进行处理，跳转到登录页

# axios

createInstance底层根据默认设置 新建一个Axios对象， axios中所有的请求[axios, axios.get,axios.post等...]内部调用的都是Axios.prototype.request,将Axios.prototype.request的内部this绑定到新建的Axios对象上,从而形成一个axios实例。新建一个Axios对象时，会有两个拦截器，request拦截器，response拦截器。

1、请求拦截器
 请求拦截器的作用是在请求发送前进行一些操作，例如在每个请求体里加上token，统一做了处理如果以后要改也非常容易。

```jsx
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么，例如加入token
    .......
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });
```

2、响应拦截器
 响应拦截器的作用是在接收到响应后进行一些操作，例如在服务器返回登录状态失效，需要重新登录的时候，跳转到登录页。

```jsx
axios.interceptors.response.use(function (response) {
    // 在接收响应做些什么，例如跳转到登录页
    ......
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

## 特点

1. Axios 是一个基于 promise 的 HTTP 库，支持promise所有的API
2. 它可以拦截请求和响应
3. 它可以转换请求数据和响应数据，并对响应回来的内容自动转换成 JSON类型的数据
4. 安全性更高，客户端支持防御 XSRF

## 方法

1. axios.get(url[, config])   //get请求用于列表和信息查询
2. axios.delete(url[, config])  //删除
3. axios.post(url[, data[, config]])  //post请求用于信息的添加
4. axios.put(url[, data[, config]])  //更新操作

## axios相关配置属性

1.  `url`是用于请求的服务器URL
2.  `method`是创建请求时使用的方法,默认是get
3.  `baseURL`将自动加在`url`前面，除非`url`是一个绝对URL。它可以通过设置一个`baseURL`便于为axios实例的方法传递相对URL
4.  `transformRequest`允许在向服务器发送前，修改请求数据，只能用在'PUT','POST'和'PATCH'这几个请求方法
5.  `headers`是即将被发送的自定义请求头
    headers:{'X-Requested-With':'XMLHttpRequest'},
6.  `params`是即将与请求一起发送的URL参数，必须是一个无格式对象(plainobject)或URLSearchParams对象
    params:{
    ID:12345
    },
7.  `auth`表示应该使用HTTP基础验证，并提供凭据
    这将设置一个`Authorization`头，覆写掉现有的任意使用`headers`设置的自定义`Authorization`头
    auth:{
    username:'janedoe',
    password:'s00pers3cret'
    }

# webpack

webpack是基于模块化的打包（构建）工具，它把一切视为模块（js、css、图片）

## 作用

- 代码转换：将TypeScript编译成JavaScript，将SCSS编译成CSS等。
- 文件优化：压缩JavaScript、CSS、HTML代码，压缩合并图片等。
- 代码分割：提取多个页面的公共代码，提取首屏不需要执行部分的代码让其异步加载。
- 模块合并：采用模块化的项目里会有很多模块文件，通过构建功能模块分类合并成一个文件。
- 自动刷新：监听本地源代码的变化，自动重新构建、刷新浏览器。

- 代码校验：在代码被提交到仓库前需要校验代码是否符合规范，以及单元测试是否通过。
- 自动发布：更新代码后，自动构建出线上发布代码并传输给发布系统。

## webpack的构建流程

Webpack 的运行流程是一个串行的过程，从启动到结束会依次执行以下流程：

1. 初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数；
2. 开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译；
3. 确定入口：根据配置中的 entry 找出所有的入口文件；
4. 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理；
5. 完成模块编译：在经过第4步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系；
6. 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会；
7. 输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。

在以上过程中，Webpack 会在特定的时间点广播出特定的事件，插件在监听到感兴趣的事件后会执行特定的逻辑，并且插件可以调用 Webpack 提供的 API 改变 Webpack 的运行结果。

## webpack模块化机制

webpack是基于commonJS的，（当然也兼容写AMD，不过不推荐）下面是commonJS 的模块写法：

```js
//输入模块
const moduleInput = require('moduleInpu')

//输出模块
module.exports = {
 ...
}
```

webpack并不强制你使用某种模块化方案，而是通过兼容所有模块化方案让你无痛接入项目

- 可以兼容多模块风格，无痛迁移老项目。
- 一切皆模块，js/css/图片/字体都是模块。
- 静态解析，按需打包，动态加载。

```jsx
require("./style.css");
require("./style.less");
require("./template.jade");
require("./image.png");
```

## 区分环境

有些时候，我们需要针对生产环境和开发环境分别书写webpack配置

为了更好的适应这种要求，webpack允许配置不仅可以是一个对象，还可以是一个**函数**

**npx webpack --env.prod**

```js
// webpack.config.js
module.exports = env => {
    if(env && env.prod) {
      return {
        mode: 'production',
        devtool: 'none'
      }
    }else {
      return {
        mode: 'development',
        devtool: 'source-map'
      }
    }
}
```

## 常见的loader

- `vue-loader` 加载和转译 Vue 组件
- [`style-loader`](https://www.webpackjs.com/loaders/style-loader) 将模块的导出作为样式添加到 DOM 中
- [`css-loader`](https://www.webpackjs.com/loaders/css-loader) 解析 CSS 文件后，使用 import 加载，并且返回 CSS 代码
- [`html-loader`](https://www.webpackjs.com/loaders/html-loader) 导出 HTML 为字符串，需要引用静态资源
- `markdown-loader` 将 Markdown 转译为 HTML
- [`script-loader`](https://www.webpackjs.com/loaders/script-loader) 在全局上下文中执行一次 JavaScript 文件（如在 script 标签），不需要解析
- [`json-loader`](https://www.webpackjs.com/loaders/json-loader) 加载 [JSON](http://json.org/) 文件（默认包含）

## loader

`loader`是文件加载器，能够加载资源文件，并对这些文件进行一些处理，诸如编译、压缩等，最终一起打包到指定的文件中。

## plugin

`plugin`功能更强大，`loader`不能做的都是它做。它的功能要更加丰富。从打包优化和压缩，到重新定义环境变量，功能强大到可以用来处理各种各样的任务。但是 plugin 是作用于webpack本身上的。

# Vue CLI

## 初始化

- Vue CLI2初始化项目

  `vue init webpack my-project`

- Vue CLI3初始化项目

  `vue create my-project`

## 构建选项

Vue CLI2

[![I46Qwd.png](https://z3.ax1x.com/2021/11/17/I46Qwd.png)](https://imgtu.com/i/I46Qwd)

Vue CLI3

[![I4c1uF.png](https://z3.ax1x.com/2021/11/17/I4c1uF.png)](https://imgtu.com/i/I4c1uF)

## 目录结构

Vue CLI2

[![I46dmQ.png](https://z3.ax1x.com/2021/11/17/I46dmQ.png)](https://imgtu.com/i/I46dmQ)

Vue CLI3

[![I4cwjO.png](https://z3.ax1x.com/2021/11/17/I4cwjO.png)](https://imgtu.com/i/I4cwjO)

## Runtime-Compiler和Runtime-only的区别

如果在之后的开发中，你依然使用template，就需要选择Runtime-Compiler

如果你之后的开发中，使用的是.vue文件夹开发，那么可以选择Runtime-only

## npm run build和dev区别

package.json里面

```json
"dev": "node build/dev-server.js", 
"build": "node build/build.js",
```

运行”npm run dev”的时候执行的是build/dev-server.js文件。用来运行项目

运行”npm run build”的时候执行的是build/build.js文件。发布前打包项目

## 修改配置起别名

在`webpack.base.conf.js`中

[![I4gqdH.png](https://z3.ax1x.com/2021/11/17/I4gqdH.png)](https://imgtu.com/i/I4gqdH)

# MVVM（Model-View-ViewModel）

<img src="https://upload-images.jianshu.io/upload_images/2002187-ddcaae06ec00dadb.png?imageMogr2/auto-orient/strip|imageView2/2/w/673/format/webp" alt="img"  />

**比MVC架构中多了一个ViewModel**，就是这个ViewModel，他是MVVM相对于MVC改进的核心思想。

Model：数据模型

View：界面视图

ViewModel：Model与Controlller之间的桥梁

Controller中的代码变得非常少，变得易于测试和维护，只需要**Controller和ViewModel做数据绑定**即可

## 实现思路

![img](https://static.oschina.net/uploads/space/2017/0521/144435_clYy_2912341.png)

1. 实现一个Observer，对数据进行劫持，通知数据的变化
2. 实现一个Compile，对指令进行解析，初始化视图，并且订阅数据的变更，绑定好更新函数
3. 实现一个Watcher，将其作为以上两者的一个中介点，在接收数据变更的同时，让Dep添加当前Watcher，并及时通知视图进行update
4. 实现MVVM，整合以上三者，作为一个入口函数

# Vue生命周期

## 创建阶段

- **beforeCreate**：实例刚在内存中创建出来，还没有初始化data和methods，只包含一些自带的生命周期函数
- **created**：实例已经在内存中创建完成，此时data和methods已经创建完成
- **beforeMount**：此时已经完成了模板的编译，只是没有渲染到界面中去
- **mounted**：模板已经渲染到了浏览器，创建阶段结束，即将进入运行阶段

## 运行阶段

- **beforeUpdate**：界面上的数据还是旧的，data数据已经更新，页面中和data还没有同步
- 中间处理过程：先根据data中的数据，在内存中渲染出一个新的DOM，当新的DOM树更新之后，会重新渲染到真实的界面中去，从而实现了从数据层到视图层的转换
- **updated**：页面重新渲染，页面中的数据和data保持一致

## 销毁阶段

- **beforeDestroy**：执行该方法的时候，Vue的生命周期已经进入销毁阶段，但是实例上的各种数据还处于可用状态
- **destroyed**：组件已经全部销毁，Vue实例已经被销毁，Vue中的任何数据都不可用

# 组件通信

##  父传子**props**

```vue
// section父组件
<template>
	<article :articles="articleList"></article>
</template>

<script>
import article from './article.vue'
export default {
    name: 'HelloWorld',
    components: { article },
    data() {
        retutn {
            articleList: ['红楼梦', '西游记', '三国演义']
        }
    }
}
</script>
```

```vue
// article子组件
<template>
    <span v-for="(item, index) in articles" :key="index">{{item}}</span>
</template>

<script>
export default {
    props: ['articles']
}
</script>
```

## 子传父**$emit**

`$emit`绑定一个自定义事件，父组件通过v-on监听并接受参数arg

```vue
// section父组件
<template>
	<article @onEmitIndex="onEmitIndex"></article>
</template>

<script>
import article from './article.vue'
export default {
    name: 'HelloWorld',
    components: { article },
    data() {
        return {
            currentIndex: -1
        }
    },
    methods: {
        onEmitIndex(index) {
            this.currentIndex = index
        }
    }
}
</script>
```

```vue
// article子组件
<template>
    <span v-for="(item, index) in articles" :key="index" @click="emitIndex(index)">{{item}}</span>
</template>

<script>
export default {
    data() {
    	return {
            articles: ['红楼梦', '西游记', '三国演义']
        }
    },
    methods: {
        emitIndex(index) {
            this.$emit('onEmitIndex', index)
        }
    }
}
</script>
```

##  **$children**/ **$parent**

指定已创建的实例之父实例，在两者之间创建父子关系。子实例可以用`this.$parent`访问父实例，子实例被推入父实例的`$children`数组中。

- `this.$children`的值是个数组
- `this.$parent`的值是个对象

```vue
// 父组件中
<template>
  <div class="hello_world">
    <div>{{msg}}</div>
    <com-a></com-a>
    <button @click="changeA">点击改变子组件值</button>
  </div>
</template>

<script>
import ComA from './test/comA.vue'
export default {
  name: 'HelloWorld',
  components: { ComA },
  data() {
    return {
      msg: 'Welcome'
    }
  },

  methods: {
    changeA() {
      // 获取到子组件A
      this.$children[0].messageA = 'this is new value'
    }
  }
}
</script>
```

```vue
// 子组件中
<template>
  <div class="com_a">
    <span>{{messageA}}</span>
    <p>获取父组件的值为:  {{parentVal}}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messageA: 'this is old'
    }
  },
  computed:{
    parentVal(){
      return this.$parent.msg;
    }
  }
}
</script>
```

## **provide/ inject**父子祖孙

- 父组件中通过`provide`来提供变量
- 子组件中通过`inject`来注入变量
- 不论子组件嵌套有多深，只要调用了`inject`，就可以注入`provide`中的数据

A.vue、B.vue、C.vue 其中 C是B的子组件，B是A的子组件

```vue
// A.vue
<template>
  <div>
	<comB></comB>
  </div>
</template>

<script>
  import comB from '../components/test/comB.vue'
  export default {
    name: "A",
    provide: {
      for: "demo"
    },
    components:{
      comB
    }
  }
</script>
```

```vue
// B.vue
<template>
  <div>
    {{demo}}
    <comC></comC>
  </div>
</template>

<script>
  import comC from '../components/test/comC.vue'
  export default {
    name: "B",
    inject: ['for'],
    data() {
      return {
        demo: this.for
      }
    },
    components: {
      comC
    }
  }
</script>
```

```vue
// C.vue
<template>
  <div>
    {{demo}}
  </div>
</template>

<script>
  export default {
    name: "C",
    inject: ['for'],
    data() {
      return {
        demo: this.for
      }
    }
  }
</script>
```

## **ref/ $refs**

`ref`：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例，可以通过实例直接调用组件的方法或访问数据， 我们看一个`ref` 来访问组件的例子

**`$refs` 只会在组件渲染完成之后生效，并且它们不是响应式的。**

```vue
// 子组件 A.vue
<script>
export default {
  data () {
    return {
      name: 'Vue.js'
    }
  },
  methods: {
    sayHello () {
      console.log('hello')
    }
  }
}
</script>
```

```vue
<tamplate>
	<component-a ref="comA"></component-a>	
</tamplate>
<script>
export default {
    mounted() {
        const comA = this.$refs.comA;
        console.log(comA.name); // Vue.js
        comA.sayHello(); // hello
    }
}
</script>
```

## **eventBus**

`eventBus`又称为事件总线，在vue中可以使用它来作为沟通桥梁的概念，就像是所有组件公用的事件中心，可以向该中心注册发送事件或接收事件

> eventBus也有不方便之处, 当项目较大,就容易造成难以维护的灾难

**1. 初始化**

首先需要创建一个事件总线并将其导出，以便其他模块可以使用或者监听它

```Js
// event-bus.js
import Vue from 'vue'
export const EventBus = new Vue()
```

假设有两个组件: `additionNum` 和 `showNum`,这里以兄弟组件为例:

```vue
<template>
  <div>
    <show-num-com></show-num-com>
    <addition-num-com></addition-num-com>
  </div>
</template>

<script>
import showNumCom from './showNum.vue'
import additionNumCom from './additionNum.vue'
export default {
  components: { showNumCom, additionNumCom }
}
</script>
```

**2.** `addtionNum.vue` 中**发送事件**

**`EventBus.$emit`**

```vue
<template>
  <div>
    <button @click="additionHandle">+加法器</button>    
  </div>
</template>

<script>
import {EventBus} from './event-bus.js'
console.log(EventBus)
export default {
  data(){
    return{
      num:1
    }
  },
  methods:{
    additionHandle(){
      EventBus.$emit('addition', {
        num:this.num++
      })
    }
  }
}
</script>
```

**3.** `showNum.vue` 中**接收事件**

**`EventBus.$on`**

```vue
<template>
  <div>计算和: {{count}}</div>
</template>

<script>
import { EventBus } from './event-bus.js'
export default {
  data() {
    return {
      count: 0
    }
  },
  mounted() {
    EventBus.$on('addition', param => {
      this.count = this.count + param.num;
    })
  }
}
</script>
```

这样就实现了在组件`addtionNum.vue`中点击相加按钮，在`showNum.vue`中利用传递来的num展示求和结果

**4. 移除事件监听者**

```js
import { eventBus } from 'event-bus.js'
EventBus.$off('addition', {})
```

##  **$attrs/ $listeners**

### **$attrs**

包含了父组件在子组件上设置的属性（除了`prop`传递的属性、`class` 和 `style` ），并且可以通过 `v-bind="$attrs"` 传入内部组件

```html
<div id="app">
  <base-input
    label="姓名"
    class="name-input"
    placeholder="请输入姓名"
    test-attrs="$attrs"
  ></base-input>
</div>
<script>
  Vue.component("base-input", {
    inheritAttrs: true, //此处设置禁用继承特性
    props: ["label"],
    template: `
    <label>
      {{label}}-
      {{$attrs.placeholder}}-
      <input v-bind="$attrs"/>
    </label>
    `,
    mounted: function() {
      console.log(this.$attrs);
      // {placeholder: "请输入姓名", test-attrs: "$attrs"}
    }
  });
  const app = new Vue({
    el: "#app"
  });
</script>
```

通过 `v-bind="$attrs"` 传入子组件内部的`input`标签

![img](https://upload-images.jianshu.io/upload_images/6531713-1ba08c2c30724a8f.png?imageMogr2/auto-orient/strip|imageView2/2/w/755/format/webp)

### **$listener**

它是一个对象，里面包含了作用在这个组件上所有的监听器（监听事件）

可以通过 `v-on="$listeners"` 将事件监听指向这个组件内的子元素（包括内部的子组件）。

## 总结

父子组件通信

- props/ $emit
- $parent/ $children
- provide/ inject
- ref/ $refs
- $attrs/ $listeners

兄弟组件通信

- eventBus
- vuex

跨级通信

- eventBus
- vuex
- provide/ inject
- $atrrs/ $listener

# 观察者模式

也叫：叫发布者-订阅者模式

定义了一个对象一对多的关系，让多个观察者同时监听一个大对象，当一个大对象发生变化时，所有依赖它的对象都会得到通知。

比如：淘宝上的某商品没货了，两个人都点击了到货通知，等货到了就通知他们。

```js
// 发布者
var obj = {}

// 发布列表，是发布者的一个方法，用来存储订阅者的信息
obj.list = []

// 增加订阅者, fn为回调函数，作为传入订阅者的信息
// key值作为，每个订阅者订阅的不同商品，相同的放在一起
obj.listen = function(key, fn) {
    if (!this.list[key]) {
        this.list[key] = []
    }
    this.list[key].push(fn)
}

// 发布消息
obj.message = function () {
    var key = Array.prototype.shift.call(arguments) // 取出消息类型名称，这里是红色
    var fns = this.list[key] // 取出消息对应回调函数集合
    if (!fns || fns.length == 0) { // 如果没有订阅这个消息，直接返回
        console.log(key + "还没有上货，请静心等待...")
        return ;
    }
    for (var i = 0, fn; fn = fns[i++];) {
        fn.apply(this, arguments)
    }
}

// 订阅者接受消息
obj.listen("红色",function(size){	//订阅者
	console.log("尺寸 ：" + size);
})
obj.message("黑色",40);
obj.message("红色",40);
```

# 响应式数据的原理

整体思路：数据劫持 + 观察者模式（对象间存在一对多关系，当一个对象被修改时，则会自动通知依赖它的对象并被自动更新）

1. 把一个普通的 JavaScript 对象传入 Vue 实例作为 `data` 选项，Vue 将遍历此对象所有的 property，并使用 **Object.defineProperty** 把这些 property 全部转为 [getter/setter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_Objects#定义_getters_与_setters)
2. 在内部getter/setter让 Vue 能够追踪依赖，在 property 被访问和修改时通知变更
3. 每个组件实例都对应一个 **watcher** 实例，它会在组件渲染的过程中把“接触”过的数据 property 记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染。


## Object.defineProperty()

语法：

```reasonml
Object.defineProperty(obj, prop, descriptor)
```

参数说明：

> obj：必需。目标对象 
> prop：必需。需定义或修改的属性的名字
> descriptor：必需。目标属性所拥有的特性

返回值：

> 传入函数的对象。即第一个参数obj

形式一：数据描述

```javascript
var obj = {
    test:"hello"
}
//对象已有的属性添加特性描述
Object.defineProperty(obj,"test",{
    configurable:true | false, //目标属性是否可以被删除或是否可以再次修改特性
    enumerable:true | false, //目标属性是否可以被枚举
    value:任意类型的值,
    writable:true | false //值是否可以重写
});
//对象新添加的属性的特性描述
Object.defineProperty(obj,"newKey",{
    configurable:true | false,
    enumerable:true | false,
    value:任意类型的值,
    writable:true | false
});
```

形式二：存取器描述

当我们使用 Object.defineProperty 对数组赋值有一个新对象的时候，会执行set方法，**但是当我们改变数组中的某一项值的时候，或者使用数组中的push等其他的方法，或者改变数组的长度，都不会执行set方法**。

```js
var obj = {};
var initValue = 'hello';
Object.defineProperty(obj,"newKey",{
    get:function (){
        //当获取值的时候触发的函数
        return initValue;    
    },
    set:function (value){
        //当设置值的时候触发的函数,设置的新值通过参数value拿到
        initValue = value;
    },
    configurable: true | false,
    enumerable: true | false
    //当使用了getter或setter方法，不允许使用writable和value这两个属性
});
//获取值
console.log( obj.newKey );  //hello

//设置值
obj.newKey = 'change value';

console.log( obj.newKey ); //change value
```

- 基于**Object.defineProperty**，不具备监听数组的能力，需要重新定义数组的原型来达到响应式。
- **Object.defineProperty** 无法检测到对象属性的添加和删除 。
- 由于Vue会在初始化实例时对属性执行getter/setter转化，所有属性必须在data对象上存在才能让Vue将它转换为响应式。
- 深度监听需要一次性递归，对性能影响比较大。

## Proxy(Vue3.0)

- 基于**Proxy**和**Reflect**，可以原生监听数组，可以监听对象属性的添加和删除。
- 不需要一次性遍历data的属性，可以显著提高性能。
- Proxy是ES6新增的属性，有些浏览器还不支持,只能兼容到IE11 。

Proxy对象用于创建一个对象的代理，从而实现基本操作的拦截和自定义（如属性查找、赋值、枚举、函数调用等）

在以下简单的例子中，当对象中不存在属性名时，默认返回值为 `37`。下面的代码以此展示了 [`get`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy/get) handler 的使用场景。

```js
const handler = {
    get: function(obj, prop) {
        return prop in obj ? obj[prop] : 37;
    }
};

const p = new Proxy({}, handler);
p.a = 1;
p.b = undefined;

console.log(p.a, p.b);      // 1, undefined
console.log('c' in p, p.c); // false, 37
```

**实现响应式**

```js
const proxyData = new Proxy(data, {
   get(target,key,receive){ 
     // 只处理本身(非原型)的属性
     const ownKeys = Reflect.ownKeys(target)
     if(ownKeys.includes(key)){
       console.log('get',key) // 监听
     }
     const result = Reflect.get(target,key,receive)
     return result
   },
   set(target, key, val, reveive){
     // 重复的数据，不处理
     const oldVal = target[key]
     if(val == oldVal){
       return true
     }
     const result = Reflect.set(target, key, val,reveive)
     console.log('set', key, val)
     return result
   },
   deleteProperty(target, key){
     const result = Reflect.deleteProperty(target,key)
     console.log('delete property', key)
     console.log('result',result)
     return result
   }
 })

  // 声明要响应式的对象,Proxy会自动代理
 const data = {
   name: "zhangsan",
   age: 20,
   info: {
     address: "杭州" // 需要深度监听
   },
   nums: [10, 20, 30]
 };
```

# Vue如何检测数组变化

考虑性能原因没有用`defineProperty`对数组的每一项进行拦截，而是选择对7中数组方法（push,shift,pop,splice,unshift,sort,reverse）进行重写(AOP 切片思想)

**所以在 Vue 中修改数组的索引和长度是无法监控到的。**

需要通过以上 7 种变异方法修改数组才会触发数组对应的 watcher 进行更新。

还可以使用**Proxy**：对一个对象进行代理之后，将得到一个和被代理一样的对象，并且可以对这个对象完全监控。Proxy是对底层操控的拦截，相当于从一个对象的底层操作开始实现对它的监听

Vue 不能检测以下数组的变动：

1. 当你利用索引直接设置一个数组项时，例如：`vm.items[indexOfItem] = newValue`
2. 当你修改数组的长度时，例如：`vm.items.length = newLength`

举个例子：

```js
var vm = new Vue({
  data: {
    items: ['a', 'b', 'c']
  }
})
vm.items[1] = 'x' // 不是响应性的
vm.items.length = 2 // 不是响应性的
```

## Vue.set()

**不能解决对数组长度的监听响应**，要使用splice

`Vue.set(target, key, value) `方法向嵌套对象添加响应式 property

- target：要更改的数据（对象或者数组）
- key：要更改的对象或数组中的索引
- value：新的值

![img](https://upload-images.jianshu.io/upload_images/16300678-31418e431ee67019.png?imageMogr2/auto-orient/strip|imageView2/2/w/674/format/webp)

当写惯了JS之后，有可能我会想改数组中某个下标的中的数据我直接this.items[XX]就改了，如：

```jsx
btn2Click:function(){
  this.items[0]={message:"Change Test",id:'10'}
}
```

我们来看看结果：

![img](https:////upload-images.jianshu.io/upload_images/16300678-5669dc2f032a1101.png?imageMogr2/auto-orient/strip|imageView2/2/w/649/format/webp)

## this.arrList.splice

```vue
<script>
export default {
 data() {
     return {
     arrList: [1,2,3,4,5]
 };
 },
 methods: {
     changeArr() {
     // this.arrList[0] = 10;
     // 修改为：
     this.arrList.splice(0, 1, 10);
     }
 }
};
</script>
```

# v-if和v-show的区别

1. v-show只是简单的控制元素的display属性，而v-if是条件渲染，条件为假元素直接不渲染
2. v-show有更高的首次渲染开销
3. v-if有更高的切换开销
4. v-if可以搭配template使用，而v-show不行

# v-model原理

1. `vue`中双向绑定是一个指令`v-model`，可以绑定一个动态值到视图，同时视图中变化能改变该值。`v-model`是语法糖，默认情况下相于`:value和@input`。
2. 使用`v-model`可以减少大量繁琐的事 件处理代码，提高开发效率，代码可读性也更好
3. 通常在表单项上使用`v-model`
4. 原生的表单项可以直接使用`v-model`，自定义组件上如果要使用它需要在组件内绑定value并处理输入事件

**其原理实现如下：**

```html
<div id="app">
    <p>v-model绑定的数据为：{{value1}}</p>
    <input type="text" v-model="value1">

    <p>绑定的数据为：{{value2}}</p>
    <input type="text" :value="value2" @input="changeVal">
</div>
<script src="./lib/vue.js"></script>
<script>
  const vm = new Vue({
    el: '#app',
    data: {
      value1: '',
      value2: ''
    },
    methods: {
      changeVal (e) {
        this.value2 = e.target.value
      }
    }
 })
</script>
```

# Vue异步更新队列

1. Vue在观察数据变化时并不是直接更新DOM，而是开启一个队列，并缓存同一个事件中发生的所有数据改变。
2. 在缓存时会除去重复元素，从而避免不必要的计算和DOM操作。
3. 然后在下一个事件循环tick中，Vue刷新队列并执行实际（已去重）的工作。

## 去重机制

Vue的这种去重机制减少了开销，如果一个for循环来动态改变数据100次，其实它只会应用最后一个改变。

如果没有这种机制，DOM就要渲染100次。

## 异步更新队列实现的选择

Vue会根据当前浏览器环境优先使用原生的Promise.then 和MutationObserve。
如果都不支持就会采用setTimeout代替。

```html
<div id="app1">
    <div id="div" v-if="showDiv">这是一段文本</div>
    <button @click="getText">获取文本</button>
</div>  
<script>
    var app1 = new Vue({
        el: '#app1',
        data: {
            showDiv: false 
        },
        methods: {
            getText() {
                this.showDiv = true;
                var text = document.getElementById("div").innerHTML;
                console.log(text);
            }
        }
    })
</script>
```

**代码报错原因**

在执行this.showDiv = "true"时，div并没有被创建出来，直到下一个Vue事件循环时，才开始创建。

**使用异步更新队列**
Vue提供了**$nextTick**来告知DOM声明时候完成更新，我们可以在$nextTick中进行div内容的获取，修改上面的例子。

```html
<div id="app2">
    <div id="div" v-if="showDiv">这是一段文本</div>
    <button @click="getText">获取文本</button>
 </div>
<script>
	 var app2 = new Vue({
        el: '#app2',
        data: {
            showDiv: false 
        },
        methods: {
            getText() {
                this.showDiv = true;
                // 通知DOM更新完成
                this.$nextTick(function() {
                    var text = document.getElementById("div").innerHTML;
                    console.log(text);
                })
               
            }
        }
    })
</script>
```

# nextTick原理

由于`Vue`的异步更新策略导致我们对数据的修改不会立马体现到都没变化上，此时如果想要**立即获取更新后的`dom`的状态**，就需要使用这个方法。

`Vue`在更新DOM时是异步执行的。只要监听到数据变化，Vue将开启一个队列，并缓冲在同一个`Event Loop`中发生所有的数据变更。如果同一个`watcher`被多次除发，只会被推入到队列中一次，避免不必要的计算和dom操作。**`nextTick`方法会在队列中加入一个回调函数，确保该函数在前面的dom操作完成后才调用。**

它可以在DOM更新完毕之后执行一个回调。

```js
this.$nextTick(() => {
    ...
})
```

源码步骤，根据执行环境分别尝试采用：

1. 先判断Promise
2. 再判断MutationObserver（变动观察器）是监视DOM变动的接口
3. 再判断setImmediate
4. 如果以上都不行则采用setTimeout

**整体流程涉及到事件的循环（Event Loop）**

每次event loop的最后，会有一个UI render，也就是更新DOM

只要**让nextTick里的代码放在UI render步骤后面执行**，就能访问到更新后的DOM了。

**又涉及到微任务(microtask)和宏任务(macrotask)**

microtask有：Promise、MutationObserver，以及nodejs中的process.nextTick

macrotask有：setTimeout, setInterval, setImmediate, I/O, UI rendering

每一次事件循环都包含一个microtask队列，在循环结束后会依次执行队列中的microtask并移除，然后再开始下一次事件循环。

# Vnode的理解

Virtual DOM，虚拟DOM就是为了解决浏览器性能问题而被设计出来的。

若一次操作中有10次更新DOM，虚拟DOM不会立即操作DOM，而是将这10次更新的diff内容保存到本地的一个JS对象上，最终这个JS对象一次性填到DOM树上。

Vnode就是简单地用javascript来表示DOM结构

## patch的过程

**比较新旧节点，一边比较一边给真实的DOM打补丁**

1. `oldVnode === vnode `执行的结果都是 return， 不需要更新
2. VNode 节点都是 isStatic（静态的），并且` key `相同时，只要将 componentInstance 与 elm 从老 VNode 节点取过来就可以
3. 新老节点均有子节点，则对子节点进行`diff`操作，使用 `updateChildren `函数来更新子节点

### updateChildren方法

虚拟DOM 与 真实DOM 一一对应，比较从两端开始，向中间靠拢，直到`oldStartIdx > oldEndIdx` 或者 `newStartIdx > newEndIdx` 停止。最后，相同的节点不变，不同的节点进行新增，删除，修改。

## 操作真实DOM代价

**DOM操作对性能影响最大其实还是因为它导致了浏览器 的重绘（repaint）和回流（reflow）**。

**重绘**指的是页面的某些部分要重新绘制，比如颜色或背景色的修改，元素的位置和尺寸并没用改变；

**回流**则是元素的位置或尺寸发生了改变，浏览器需 要重新计算渲染树，导致渲染树的一部分或全部发生变化。

如下的这些DOM操作会导致回流:

- 增加、删除和修改可见DOM元素
- 页面初始化的渲染
- 移动DOM元素
- 修改CSS样式，改变DOM元素的尺寸
- DOM元素内容改变，使得尺寸被撑大
- 浏览器窗口尺寸改变
- 浏览器窗口滚动

**什么情况下操作元素不会引起重排**：元素脱离文档流时

# v-for中key的作用

- 为了更高效的对比虚拟DOM中每个节点是否是相同的节点
- Vue在patch的过程中判断两个节点是否是相同节点，key是一个必要条件，如果不定义key的话，Vue只能认为比较的两个节点是同一个，这导致了频繁的更新元素，使得整个patch过程比较低效
- Vue判断两个节点是否相同，主要是通过判断两者的key和元素类型，因此不设key，它的值就是undefined，则可能永远认为这两个是相同的节点

# computed和watch的区别

**computed**是计算属性，依赖其他属性计算值，computed的值有缓存，只有当依赖的属性变化才会返回内容，它可以设置getter和setter。

一个值依赖多个属性（多对一），用**computed**更方便

计算属性默认只有 getter，不过在需要时你也可以提供一个 setter：

```js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```

现在再运行 `vm.fullName = 'John Doe'` 时，setter 会被调用，`vm.firstName` 和 `vm.lastName` 也会相应地被更新。

**watch**是侦听一个特定的值，当这个值变化时执行特定的函数。

一个值变化会引起一系列操作（一对多），用**watch**更方便

# Vuex

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**

状态管理模式其实是 集中式存储管理应用的所有组件的状态。

使用场景：多个组件共享数据或者是跨组件传递数据时

每一个 Vuex 应用的核心就是 **store（仓库）**，它包含着你的应用中大部分的**状态 (state)**。

1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地**提交 (commit) mutation**。这样使得我们可以方便地跟踪每一个状态的变化。

[安装](https://vuex.vuejs.org/zh/installation.html) Vuex 之后，让我们来创建一个 store。创建过程直截了当——仅需要提供一个初始 state 对象和一些 mutation：

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```

现在，你可以通过 `store.state` 来获取状态对象，以及通过 `store.commit` 方法触发状态变更：

```js
store.commit('increment')

console.log(store.state.count) // -> 1
```

**为了在 Vue 组件中访问 `this.$store` property**，你需要为 Vue 实例提供创建好的 store。Vuex 提供了一个从根组件向所有子组件，以 `store` 选项的方式“注入”该 store 的机制：

```js
new Vue({
  el: '#app',
  store: store,
})
```

现在我们**可以从其他组件的方法提交一个变更**：

```js
methods: {
  increment() {
    this.$store.commit('increment')
    console.log(this.$store.state.count)
  }
}
```

## state

vuex的基本数据，用来存储变量

## getters

从基本数据(state)派生的数据，相当于state的计算属性，Getter 会暴露为 `store.getters` 对象

- 以属性的形式访问：

  ```js
  store.getters.doneTodos // -> [{ id: 1, text: '...', done: true }]
  ```

  **getter 在通过属性访问时是作为 Vue 的响应式系统的一部分缓存其中的**

- 通过方法访问：

  你也可以通过让 getter 返回一个函数，来实现给 getter 传参。在你对 store 里的数组进行查询时非常有用。

  ```js
  getters: {
    // ...
    getTodoById: (state) => (id) => {
      return state.todos.find(todo => todo.id === id)
    }
  }
  store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
  ```

  注意，**getter 在通过方法访问时，每次都会去进行调用，而不会缓存结果**。

state和getters的辅助函数，在组件中使用:

```js
import { mapState, mapGetters } from 'vuex'
computed: {
  ...mapState({ // mapState 辅助函数帮助我们生成计算属性
    countAlias: 'count',
  }),
  ...mapGetters({ // mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性
    thisDoneCount: 'doneTodosCount'
  })
}
```

## mutations

**提交更新数据的方法，必须是同步的(**如果需要异步使用action)。每个mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数，提交载荷作为第二个参数。

你可以向 `store.commit` 传入额外的参数，即 mutation 的 **载荷（payload）**：

**在大多数情况下，载荷应该是一个对象（也可以是一个参数）**，这样可以包含多个字段并且记录的 mutation 会更易读：

```js
// ...
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```

```js
store.commit('increment', {
  amount: 10
})
```

mutations的辅助函数，在组件中提交Mutation

```js
import { mapMutations } from 'vuex'
export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

      // `mapMutations` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}
```

## action

和mutation的功能大致相同，不同之处在于：1. Action 提交的是 mutation，而不是直接变更状态。 2. Action 可以包含任意异步操作。

Action 通过 `store.dispatch` 方法触发：

```js
store.dispatch('increment')
```

我们可以在 action 内部执行**异步**操作：

```js
actions: {
  incrementAsync ({ commit }, payload) {
    setTimeout(() => {
      commit('increment', {
        amount: payload.amountAsync
      })
    }, 1000)
  }
}
```

Actions 支持同样的载荷方式和对象方式进行分发：

```js
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amountAsync: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amountAsync: 10
})
```

在组件中分发 Action

你在组件中使用 `this.$store.dispatch('xxx')` 分发 action，或者使用 `mapActions` 辅助函数将组件的 methods 映射为 `store.dispatch` 调用（需要先在根节点注入 `store`）：

```js
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

## modules

模块化vuex，可以让每一个模块拥有自己的state、mutation、action、getters,使得结构非常清晰，方便管理。

对于模块内部的 action，局部状态通过 `context.state` 暴露出来，根节点状态则为 `context.rootState`：

```js
const moduleA = {
  // ...
  actions: {
    incrementIfOddOnRootSum ({ state, commit, rootState }) {
      if ((state.count + rootState.count) % 2 === 1) {
        commit('increment')
      }
    }
  }
}
```

对于模块内部的 getter，根节点状态会作为第三个参数暴露出来：

```js
const moduleA = {
  // ...
  getters: {
    sumWithRootCount (state, getters, rootState) {
      return state.count + rootState.count
    }
  }
}
```

### 命名空间

默认情况下，模块内部的 action、mutation 和 getter 是注册在**全局命名空间**的——这样使得多个模块能够对同一 mutation 或 action 作出响应。

如果希望你的模块具有更高的封装度和复用性，你可以通过添加 `namespaced: true` 的方式使其成为带命名空间的模块。当模块被注册后，它的所有 getter、action 及 mutation 都会自动根据模块注册的路径调整命名。

```js
const store = new Vuex.Store({
  modules: {
    account: {
      namespaced: true,

      // 模块内容（module assets）
      state: () => ({ ... }), // 模块内的状态已经是嵌套的了，使用 `namespaced` 属性不会对其产生影响
      getters: {
        isAdmin () { ... } // -> getters['account/isAdmin']
      },
      actions: {
        login () { ... } // -> dispatch('account/login')
      },
      mutations: {
        login () { ... } // -> commit('account/login')
      },

      // 嵌套模块
      modules: {
        // 继承父模块的命名空间
        myPage: {
          state: () => ({ ... }),
          getters: {
            profile () { ... } // -> getters['account/profile']
          }
        },
        // 进一步嵌套命名空间
        posts: {
          namespaced: true,
          state: () => ({ ... }),
          getters: {
            popular () { ... } // -> getters['account/posts/popular']
          }
        }
      }
    }
  }
})
```

# Vue Router原理

通过改变URL，在不重新请求页面的情况下，更新页面视图。

**更新视图但不重新请求页面**，是前端路由原理的核心之一

在浏览器环境中实现这一功能有2种方式：

1. Hash：利用URL中的hash("#")
2. History interface：HTML5中新增的方法

Vue中，通过`mode`这一参数控制路由的实现模式

```js
const router = new VueRouter({
    mode: 'history',
    routes: [...]
})
```

**`mode`参数：**

1. 默认hash（http://localhost:8080/#/login）
2. history，如果浏览器不支持则采用hash（http://localhost:8080/login）
3. abstract，在Node环境下

## HashHistory

hash("#") 的作用是加载 URL 中指示网页中的位置。

\# 本身以及它后面的字符称之为 hash，可通过 **window.location.hash** 获取

特点：

1. hash虽然在url中，但不会被包括在http请求中，它是用来指导浏览器动作的，对服务端完全没用，因此改变hash不会重新加载页面。
2. 可以为 hash 的改变添加监听事件：`window.addEventListener("hashchange",funcRef,false)`
3. 每一次改变 hash(window.localtion.hash)，都会在浏览器访问历史中增加一个记录。

**HashHistory.push()** 将新路由添加到浏览器访问历史的栈顶

**HashHistory.replace()** 将新路由替换掉当前的路由



## HTML5History

**History interface** 是浏览器历史记录栈提供的接口，通过back()、forward()、go()等方法，我们可以读取浏览器历史记录栈的信息，进行各种跳转操作。

从 HTML5开始，**History interface** 提供了2个新的方法：pushState()、replaceState() 使得我们可以对浏览器历史记录栈进行修改：

1. `window.history.pushState(stateObject,title,url)`
2. `window.history.replaceState(stateObject,title,url)`

参数：

1. stateObject：当浏览器跳转到新的状态时，将触发 Popstate 事件，该事件将携带stateObject 参数的副本
2. title：所添加记录的标题
3. url：所添加记录的 url

这`2`个方法有个共同的特点：当调用他们修改浏览器历史栈后，虽然当前`url`改变了，但浏览器不会立即发送请求该`url`，这就为单页应用前端路由，更新视图但不重新请求页面提供了基础。

1. push与hash模式类似，只是将window.hash改为history.pushState
2. replace与hash模式类似，只是将window.replace改为history.replaceState
3. 监听地址变化在HTML5History的构造函数中监听popState（window.onpopstate） 

## 两种模式比较

pushState设置的新URL可以是与当前URL同源的任意URL；hash只能修改#后面的部分，故只可设置与当前同文档的URL

pushState通过stateObject可以添加任意类型的数据到记录中；而hash只可添加短字符串

pushState可设置额外的title属性供后续使用

history模式会将URL修改的和正常请求后端的URL一样，如果后端没有配置对应/user/id的路由处理，则会返回404错误

# Vue Router跳转到新的窗口

## 1 不带参

1.1 router-link

```html
<router-link :to="{name:'home'}"> 
<router-link :to="{path:'/home'}"> 
//name,path都行, 建议用name  
// 注意：router-link中链接如果是'/'开始就是从根路由开始，如果开始不带'/'，则从当前路由开始。
```

1.2 this.$router.push()

```javascript
this.$router.push('/home') 
this.$router.push({name:'home'}) 
this.$router.push({path:'/home'})
```

1.3 this.$router.replace() (用法同push)

## 2 带参

2.1 router-link

```html
<router-link :to="{name:'home', params: {id:1}}"></router-link>
// params传参数 (类似post)
// 路由配置 path: "/home/:id" 或者 path: "/home:id" 
// 不配置path,第一次可请求,刷新页面id会消失
// 配置path,刷新页面id会保留

<router-link :to="{name:'home', query: {id:1}}"> 
// query传参数 (类似get,url后面会显示参数)
// 路由可不配置
```

2.2 this.$router.push

```js
// query传参
this.$router.push({name:'home',query: {id:'1'}})
this.$router.push({path:'/home',query: {id:'1'}})
// 跳转到的页面接受参数
this.id = this.$route.query.id

// params传参
this.$router.push({name:'home',params: {id:'1'}})  
// 跳转到的页面接受参数
this.id = this.$route.params
// 只能用 name
// 路由配置 path: "/home/:id" 或者 path: "/home:id" ,
// 不配置path ,第一次可请求,刷新页面id会消失
// 配置path,刷新页面id会保留
 
```

2.3 this.$router.replace() (用法同push)

## this.$router.go(n)

his.router.go(n) 向前或者向后跳转n个页面，n可为正整数或负整数

区别：

this.$router.push 跳转到指定url路径，并向history栈中添加一个记录，点击后退会返回到上一个页面

this.$router.replace 跳转到指定url路径，但是history栈中不会有记录，点击返回会跳转到上上个页面 (就是直接替换了当前页面)

this.$router.go(n) 向前或者向后跳转n个页面，n可为正整数或负整数

## window.open

```javascript
// 开始页
let id = item.id
let routeData = this.$router.resolve({path: '/res/imgDetail', query: {ID: id}})
window.open(routeData.href, '_blank')

// 跳转到的页面接受参数
this.id = this.$route.query.ID
```

