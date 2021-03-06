# 自我介绍

面试官您好，我叫郭威龙，来自云南师范大学软件工程专业，我的家乡是湖北荆州。自己对前端很感兴趣，并且经过系统性的学习，所以想从事前端开发。之前有幸参与了一个中国烟草内部系统的开发，该系统运行在中烟技术中心内网，（功能总体由“卷烟产品包装互动协同系统”与“卷烟产品包装装潢设计资源库”两大部分组成）。然后我负责了互动协同系统中的专家库部分以及设计资源库的开发。加快了项目完成的进度。在平时的学习中，我也善于归纳解决问题，会以写博客的方式记录学过的知识和技术。

（云产卷烟新品美学互动设计系统）
卷烟产品包装装潢  设计资源库主页以及资源详情页。
Vue 2.6.x
Axios 0.21.0
Element 2.14.x



（小程序）
遇到的问题：在各个功能中用户要能删除自己发布的信息。
期望的效果：界面上是自己发的信息就有删除按钮，他人发的就没有删除按钮。
所以需要用小程序的openid进行比对判断是否渲染删除按钮，那么用户在登陆后需要每个页面都能获取到用户的openid。由于小程序中没有传统的cookie机制，这时就需要采用wx.setStorage将调用登录云函数返回的openid进行缓存，然后在需要openid的页面就可以采用wx.getStorage获取到用户的openid，就可以与每一条发布的信息的openid进行比对了，相同的则是自己发的信息，就渲染出删除按钮。

# 实习困难

实习中组长将一个功能模块（专家库）给到我和另一个后端实习生，因为文档上只说了要实现哪些功能，具体的实现效果没有说，然后就得自己去设计。

例如在新增专家表单时，文档上要求专家详情信息中要有个人信息、工作经历、教育背景、所获荣誉，一开始都不确定应该传给后端什么样的数据结构，

后面经过思考，因为每个专家，都可能会有多条工作经历、教育背景和所获荣誉，所以在新增表单的对象结构中这三个属性对应的值应该是一个数组类型，然后数组里每个元素又是一个对象。

在确定了提交表单的结构后，和后端沟通了后端就开始写接口。

## 与后端数据交互格式

**json**

基本类型：{“键” : 值, “键” : “值”,…}

数组类型：[{“键” : 值, “键” : “值”},{“键” : 值, “键” : “值”},…]

对象嵌套：

```json
{
    “name”: “teacher”,
    “computer”: {
        “CPU”:"intel7,
        “disk”: “512G”
    },
    “students”: [
        {
        “name”: “张三”,
        “age”: 18,
        “sex”: true
        },
        {
        “name”: “李四”,
        “age”: 19,
        “sex”: false
        }
    ]
}
```



# 未来规划 

- 短期：1年内，进入公司，接触到开发流程，需求->开发->测试，熟悉技术栈 
- 中期：1-3年，从保住饭碗到熟练工的过程，熟悉业务，个人有承担模块搭建流程，决定开发方向的能力 
- 长期：3-5年，专注于感兴趣的方向，深耕行业中某一细化分支的业务逻辑，比如富文本，echart等，成为这一领域的专家

# 自己的优点

我觉得我比较沉着冷静，无论在做任何事情的时候，我都会再三思考，权衡利弊，把所有发生问题的可能性都想一遍。因为我希望我自己永远都不会有处于绝境的时候。

然后我做事也很有计划性，保证按时完成计划事情之外，还会对完成的事情有自己更好的追求

性格比较温和，为人很和善，善于与人沟通交流，可以很好的与同事以及领导相处，高效的完成项目

# 自己的缺点

容易想很多，不管是面对生活上的事，还是工作上的事，其实有时候处理一个事情没有我想象的那么复杂，有时候我就会想的钻进去，直到想清楚事情的起因和所有可能的后果。这也导致有时候有人会说我犹豫不决。我也希望我以后能在有些可以快速处理的事情上更果断一点，然后在需要谨慎处理的事上多多考虑。

# 最具有挑战的困难的事

高考前100天，把英语从60分左右的水平提升到了接近120的水平。

# 对联易融的了解

联易融致力于通过科技和创新来重新定义和改造供应链金融，成为全球领先的供应链金融科技解决方案提供商。

联易融响应国家普惠金融的号召，聚焦于ABCD（AI、区块链、云计算、大数据）等先进技术在供应链生态的应用，以线上化、场景化、数据化的方式提供创新供应链金融科技解决方案。

我们的云原生解决方案，可优化供应链金融的支付周期、实现供应链金融全流程的数字化，提升整个供应链金融生态系统的透明度和连通性，支持实体经济。

# 反问

薪资体系结构和工作环境
