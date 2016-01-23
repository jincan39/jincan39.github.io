---
layout: post
title: 网站开发普及
excerpt: "Website Development."
author: Channing
modified: 2016-01-23
tags: [Website, Programming]
comments: true
---
{% include _toc.html %}


## 网站开发普及


### 趣文：[编程语言伪简史](http://www.oschina.net/news/41233/brief-incomplete-and-mostly-wrong)


1. 概述：
               [一个网站的构造](http://www.1ke.co/course/30)

2.正文

核心：耦合度 ，开发效率的考虑
大型程序的构建，敏捷开发和部署  需要保证各个功能模块相对独立；前后端也需要分离

一.架构
单体式应用至微服务化的演变

[单体式	:](http://dockerone.com/uploads/article/20150524/89d9bfed11ff35943269b24b23b866b1.png)

之前：尽管也是模块化逻辑，但是最终它还是会打包并部署为单体式应用。具体的格式依赖于应用语言和框架。例如，许多Java应用会被打包为WAR格式，部署在Tomcat或者Jetty上，而另外一些Java应用会被打包成自包含的JAR格式，同样，Rails和Node.js会被打包成层级目录。应用无法扩展，可靠性很低，最终，敏捷性开发和部署变的无法完成。

（基于Docker的）[微服务化：](http://dockerone.com/uploads/article/20150524/858f9ae6c861c8c93cd5379be54f9fc1.png)


目前：每一个应用功能区都使用微服务完成，另外，Web应用会被拆分成一系列简单的Web应用（比如一个对乘客，一个对出租车驾驶员）。这样的拆分对于不同用户、设备和特殊应用场景部署都更容易。
             微服务的目的是有效的拆分应用，实现敏捷开发和部署。微服务应用是分布式系统，由此会带来固有的复杂性，对于程序员的要求更高。~

详情： [http://dockone.io/article/394](http://dockone.io/article/394)




二.前后端

**[MVC](https://zh.wikipedia.org/wiki/MVC)模式**（Model-View-Controller）
一种[软件架构](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E6%9E%B6%E6%9E%84)模式，把软件系统分为三个基本部分：模型（Model）、视图（View）和控制器（Controller）。
    其中： Model是用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法，有对数据直接访问的权力，例如对数据库的访问。
     过去十年，用于构造网站的”MV*框架”如同雨后春笋一般层出不穷，但都不愿意面对或者解决的问题是，它对前端设计师极不友好，而且，开发效率及其低下。
          前后端的耦合度太高了，为了解决这一问题，我们在Model层之上引入Service层：
![](http://images.cnitblog.com/blog/306623/201401/231951107414.png)
           目前大部分系统的架构图，虽然有些系统采用分布式架构，层与层之间使用了远程调用框架，但是本质上都逃不开上面这个架构设计。
          这张图是一张比较合理的图，在实际开发里最常发生的事情就是控制层（Control）越过服务层（Service）直接处理下面的资源。
           前后端耦合的问题主要发生在控制层（Control），控制层是前端和服务端交互的边界，但是在开发过程中控制层（Control）和服务层（Service）常常混淆不清，这就是前后端耦合度高的重要原因。

详情：[http://www.cnblogs.com/sharpxiajun/p/3531665.html](http://www.cnblogs.com/sharpxiajun/p/3531665.html)


**至此**：
           前端通过html和css，以及js表达自己的想法，后端只负责一件事情，把前端需要的数据填上去，是的，就是填数据而已，所以只有后端看不懂前端的数据应该填在哪儿，或者应该填什么数据的时候，才会需要有限的交流。

工作流程：

1. 任务书或者bug ticket下来，前端开branch，开始做或者改页面
2. 如果是页面的bug对应，通常到这一步就已经结束了，如果是新功能，或者bug需要后端协作，那么ticket转给后端
3. 后端拿到ticket，开工干活，完事，push。
4. release




三.如何完成前后端分离
              前后端分离的例子就是SPA(Single-page application)，所有用到的展现数据都是后端通过异步接口(AJAX/JSONP)的方式提供的，前端只管展现。（这句话可以翻译成**用了前端框架，并使用了Restful的架构思想**）
              从某种意义上来说，SPA（有哪些前端框架可以做SPA？请看：http://todomvc.com/）确实做到了前后端分离，但这种方式存在两个问题：

* WEB服务中，SPA类占的比例很少。很多场景下还有同步/同步+异步混合的模式，SPA不能作为一种通用的解决方案。
* 现阶段的SPA开发模式，接口通常是按照展现逻辑来提供的，有时候为了提高效率，后端会帮我们处理一些展现逻辑，这就意味着后端还是涉足了View层的工作，不是真正的前后端分离。

           在业务逻辑复杂的系统里，我们最怕维护前后端混杂在一起的代码，因为没有约束，M-V-C每一层都可能出现别的层的代码，日积月累，完全没有维护性可言。
          虽然前后端分离没办法完全解决这种问题，但是可以大大缓解。因为从物理层次上保证了你不可能这么做。
因此，淘宝引入了Nodejs来做Node的全栈开发，并将之作为”中途岛”：（虽然nodejs可以做全栈，为了保证物理层次上的分离，而且淘宝基于JAVA的基础架构已经非常强大而且稳定，更适合做现在架构的事情。）

 

Nodejs双11稳定性：https://www.zhihu.com/question/37379084


四.[前端发展 ](http://chan.science/%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E6%8A%80%E6%9C%AF%E7%9A%84%E5%8F%91%E5%B1%95/)
对于前端：
jQuery的思维方式是：以DOM操作为中心
MV*框架的思维方式是：以模型为中心，DOM操作只是附加


Facebook认为MVC无法满足他们的扩展需求，因此他们决定使用另一种模式：[Flux] (http://www.tuicool.com/articles/MjUrMn)。
          这一思想上文中说到的前后端MVC架构中引入Service层很像，因为程序员在开发过程中控制层（Control）和服务层（Service）常常混淆不清，导致的模块间耦合度过高，后续推动困难。

他们重新发明了真正的MVC，并且强调了数据单向流的概念。

          Flux 通过严格的控制数据的更新来实现单向数据流，消除了数据双向绑定的Side Effect，这样的好处是你能清晰的掌握数据的改变方式及相应代码的位置。保证自己的程序不会因为业务的发展变得越来越臃肿。（试想在一个项目有几十上百个 Component 的情况下每个 Component 都可能改变了数据，那处理起来可就麻烦大了！）
目前Flux的解决方案有如下：https://github.com/voronianski/flux-comparison

[React](http://reactjs.cn/react/docs/why-react.html)：
             React 是一个 Facebook 和 Instagram 用来创建用户界面的 JavaScript 库。他仅仅是View层，并使用了Virtual DOM的技术。
            通过 React 你唯一要做的事情就是构建组件。得益于其良好的封装性，组件使代码复用、测试和关注分离（separation of concerns）更加简单。

React信奉** **[Unix 哲学](https://en.wikipedia.org/wiki/Unix_philosophy) ，而Unix 已接受住了时间的考验，原因是：

*拥有小、可组装性、目的单一的思想的工具永远不会落伍。*

你可以自由选择当下最好的库来最优地解决你的问题。JavaScript 发展很快，而 React 允许你用更好的库来替换你的应用程序的局部，而不是等待和期盼你的框架做创新。（当然这也需要程序员拥有更多的创新意识）


Angular：
分[Angular1](https://docs.google.com/document/d/1Ma8baPpeS-MPgvaqybiPa-6b2HQMrGEzSb1wR0mpUDA/edit#)和[Angular2](https://docs.google.com/document/d/19_9pshmkAQOA67UWTm41bzWbvikwerVjnCD97D0JS7g/edit#) ，从模块化到组件化
Angular2采用了Typescript并且借鉴了React的思想引入了组件化WebComponent的做法，也引入了React得数据单向流概念。使用了shadow DOM提供了 3-10 倍的性能提升。（这三点上看感觉很像React）。相比Angular1.4：

* 没有了controller
* 没有了$scope
* 没有了$apply
* 没有了数据双向绑定
* 没有了directive

[为什么要更新Anuglar2](http://www.oschina.net/translate/angular-1-vs-angular-2-a-high-level-comparison)：（确实React的思想更好）
1.数据绑定运行后：（React是数据单向流）

* 不清楚哪些监视器会运行，什么顺序，多少次
* 模型更新顺序难以推论和预期
* 摘要循环多次运行导致时间消耗

2：性能优化（采取了Shadow DOM，可能比较像React的Virtual DOM）
3：组件化  
4：简洁化（有且仅有一种依赖注入机制）

[Angular2对比React](https://www.youtube.com/watch?v=XQM0K6YG18s)

*区别：*

1. *Angular 是一个框架，React 是一个库。在 Angular 和 React 之间做选择就像选择买一个现成的电脑与选择利用现成的部件组装你自己的电脑。因此，*React 让你可以根据你选择的必需的功能来限制你的应用大小.
2. *Angular 2 将 “JS” 嵌入 HTML。React 将 “HTML” 嵌入 JS。*Angular 2 依然保留以 HTML 为中心而不是以 JavaScript 为中心。Angular 2 没有解决它本质的设计问题。
3. Angular 致力于以 HTML 为中心，相对于以简单的 JavaScript 为中心模型的 React，Angular 更复杂。使用 React，你不需要学习框架的声明 HTML 语法例如 ngxxx。
4. *Angular 2尚未成熟，国内的运用可能还需要3年左右*

至于Angular1.4，更像是对于传统前端MV*框架的一个大集合（有800多个模块）

Vue：
这是一个受Angular和React等启发的精简框架

1. 跟React一样，它也只是一个界面库
2. 它的写法相对于Angular较为接近
3. 构建[大型应用 ](http://cn.vuejs.org/guide/application.html)的思想采取了React的Flux

[为什么选择Vue而不是Angular](http://cn.vuejs.org/guide/comparison.html)
有意思的是，Angular 2 和 Vue 用相似的设计解决了一些 Angular 1 中存在的问题。




最后：由于前端仍然在一个快速发展期，所以我们需要更多的是有能力，创新和冒险精神的工程师们

ps:**对于移动开发  **
移动应用开发领域有一个BaaS(后端即服务：[Backend as a Service](http://baike.baidu.com/link?url=ddIZmWYWygM5J9Ms24kLsEPF1ay2Gq4tRcwih2zQ1r_wwXWpR-0dCZ3V0pJ0BpvByd6xyu5RQqRiiHHZM1OXw_))的概念。这些集成服务包括：账户管理、消息推送、社交网络整合、地理位置与广告等。

