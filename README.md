# Vue-Interview

### 1.v-if和v-for哪个优先级高？如果两个同时出现，应该怎么优化得到更好的性能？

​	当v-if与v-for一起使用时，v-for具有比v-if更高的优先级，因为v-if将分别重复运行于每个v-for循环中，所以不推荐同时使用。因将v-if和v-for分别放在不同标签中。

​	如果v-if和v-for同时使用放在同一级标签中，那么可以使用计算属性进行优化得到更好的性能

```javascript
// 计算属性
computed: {
	calculateList() {
		return (params1, params2) => {
			return params1.filter(item => item.navigationbarId == JSON.parse(params2).navigationbarId);
		}
	}
}

// html 中 v-for
v-for="(row, i) in calculateList(scope.row.navDish, item)" :key="i"
```

使用计算属性进行优化好处：

* 过滤后的数组发生相关变化时才被重新运算，过滤更高效。

* 使用v-for之后，在渲染的时候只遍历需要的即可，渲染更高效。

* 解藕渲染层的逻辑，可维护性 (对逻辑的更改和扩展) 更强。



### 2.Vue组件data选项为什么必须是个函数而Vue的根实例则没有此限制？

在创建或注册模板的时候传入一个 data 属性作为用来绑定的数据。但是在组件中，data必须是一个函数，因为每一个 vue 组件都是一个 vue 实例，通过 new Vue() 实例化，引用同一个对象，如果 data 直接是一个对象的话，那么一旦修改其中一个组件的数据，其他组件相同数据就会被改变，而 data 是函数的话，每个 vue 组件的 data 都因为函数有了自己的作用域，互不干扰。



### 3.你知道vue中key的作用和工作原理吗？说说你对它的理解。

vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以标识组件的唯一性，vue.js的虚拟DOM算法，在更新vNode时，需要从旧vNode列表中查找与新vNode节点相同的vNode进行更新，如果这个过程设置了属性key，过程就会快很多。



### 4.你怎么理解vue中的diff算法

虚拟节点通过JS的Object对象模拟DOM中的节点，然后再通过特定的render方法将其渲染成真实的DOM节点 dom diff 则是通过JS层面的计算，返回一个patch对象，也就是补丁对象，在通过特定的操作解析patch对象，完成页面的重新渲染。

实现步骤：

    		* 用JavaScript对象模拟DOM
    		* 把此虚拟DOM转成真实DOM并插入页面中
    		* 如果有事件发生修改了虚拟DOM
    		* 比较两棵虚拟DOM树的差异，得到差异对象
    		* 把差异对象应用到真正的DOM树上

总结：

​	比较两棵DOM树的差异是Virtual DOM算法最核心的部分，简单的说就是新旧虚拟dom 的比较，如果有差异就以新的为准，然后再插入的真实的dom中，重新渲染。



### 5.谈一谈对vue组件化的理解？

一、基础概念
1、概念：组件是html、css、js等的一个聚合体

2、为什么要使用组件？

 1、组件化

* 将一个具备完整功能的项目的一部分进行多处使用

* 加快项目的进度

* 可以进行项目的复用

2、要想实现组件化，我们使用的这一部分必须是完整的，这个完整的整体称之为组件

3、vue将html、css、js、img等聚合体放在一起组成的文件称之为单文件组件，后缀名为vue（xxx.vue）



### 6.谈一谈对vue的设计原则的理解？

1、 容错处理, 这个要做好, 极端场景要考虑到, 不能我传错了一个参数你就原地爆炸
2、 缺省值(默认值)要有, 一般把应用较多的设为缺省值
3、 颗粒化, 把组件拆分出来.
4、 一切皆可配置, 如有必要, 组件里面使用中文标点符号, 还是英文的标点符号, 都要考虑到
5、 场景化, 如一个dialog弹出, 还需要根据不同的状态封装成success, waring, 等
6、 有详细的文档/注释和变更历史, 能查到来龙去脉, 新版本加了什么功能是因为什么
7、 组件名称, 参数prop, emit, 名称设计要通俗易懂, 最好能做到代码即注释这种程度
8、 可拓展性, 前期可能不需要这个功能, 但是后期可能会用上, 要预留什么, 要注意什么, 心里要有逼数
9、 规范化,我这个input组件, 叫on-change, 我另外一个select组件叫change, 信不信老子捶死你
10、 分阶段: 不是什么都要一期开发完成看具体业务, 如果一个select, 我只是个简单的select功能, 什么multi老子这个版本压根不需要, 别TM瞎折腾! 给自己加戏



### 7.vue为什么要求组件模板只能有一个根元素？

Vue其实并不知道哪一个才是我们的入口，因为对于一个入口来讲，这个入口就是一个"Vue类"，Vue需要把这个入口里面的所有东西拿来渲染，处理，最后再重新插入到dom中。如果同时设置了多个入口，那么vue就不知道哪一个才是这个"类"。



### 8.谈谈你对MVC、MVP和MVVM的理解？

MVC：

​	MVC全名是Model View Controller，是模型(model)－视图(view)－控制器(controller)的缩写，一种软件设计典范，用一种业务逻辑、数据、界面显示分离的方法组织代码，将业务逻辑聚集到一个部件里面，在改进和个性化定制界面及用户交互的同时，不需要重新编写业务逻辑。MVC被独特的发展起来用于映射传统的输入、处理和输出功能在一个逻辑的图形化用户界面的结构中。



MVP:

​	mvp模式主要是解决mvc中的缺点，mvp作为一种新的模式，MVP与MVC有着一个重大的区别：在MVP中View并不直接使用Model，它们之间的通信是通过Presenter (MVC中的Controller)来进行的，所有的交互都发生在Presenter内部，而在MVC中View会直接从Model中读取数据而不是通过 Controller。



MVVM:

​	如果说MVP是对MVC的进一步改进，那么MVVM则是思想的完全变革。它是将“数据模型数据双向绑定”的思想作为核心，因此在View和Model之间没有联系，通过ViewModel进行交互，而且Model和ViewModel之间的交互是双向的，因此视图的数据的变化会同时修改数据源，而数据源数据的变化也会立即反应到View上。



### 9.谈谈你对vue组件之间通信的理解？



### 10.你了解哪些vue性能优化方法？

一.代码包优化

	1.屏蔽sourceMap
	
	2.对项目代码中的JS/CSS/SVG(*.ico)文件进行gzip压缩
	
	3.对路由组件进行懒加载
二.源码优化

    1.v-if 和 v-show选择调用
     
    2.为item设置唯一key值
    
    3.细分vuejs组件
    
    4.减少watch的数据
    
    5.内容类系统的图片资源按需加载
    
    6.SSR(服务端渲染)

三.用户体验优化

```
1.better-click防止iphone点击延迟

2.菊花loading

3.骨架屏加载
```



### 11.你知道vue3有哪些新特性吗？它们会带来什么影响？

### 12.vue如果想扩展某个现有的组件时应该怎么做？

### 13.watch和computed的区别以及怎么选用?

### 14.谈谈你对vue生命周期的理解？

### 15.谈谈你对vuex使用及其理解？

### 16.你知道nextTick的原理吗？

### 17.你知道vue的双向数据绑定的原理吗？

### 18.vue-router导航钩子有哪些？

### 19.什么是一个递归组件？

### 20.谈一谈你对vue响应式原理的理解？














