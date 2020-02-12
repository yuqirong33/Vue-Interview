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

Vue组件之间的通信主要归类为3种：

* 父子组件之间的通信
* 任意两个组件之间的通信
* 最终的boss，Vuex-状态管理模式



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

vue3新特性：

* 更快
* 更小
* 更易于维护
* 更多原生支持
* 更易于开发使用
* 重写虚拟DOM
* 优化插槽生成
* 静态树提升
* 基于Proxy的观察者机制
* 使vue更小
  * 以es5为基础，更小更快。（快：Proxy重构虚拟dom功能，小：支持tree-shaking，运行时的最小体积将低于10kb）
  *  支持TS 3.0源码使用TS编写（Typescript）
  * 优化插槽生成：
    在当前的vue版本中，当父组件重新渲染时，其子组件也必须重新渲染（除非修改的数据是子组件的props，才会触发组件的重新渲染）。使用vue3，可以单独重新渲染父组件和子组件。
  *  静态树提升：
    使用静态树提升，这意味着vue3的编译器能够检测到什么是静态组件，然后将其提升，从而降低了渲染成本。
  * 更多原生的支持，运行时内核将与平台无关，使得vue可以更容易的与任何平台（ios、android、web）一起使用
  * 更易于开发使用，Observer模块已被解压缩到自己的包中，允许使用它。
  * 3.0 Function-based API 代替传统的Class API ,摒弃高阶组件。
    优势：复用简单，把要复用的逻辑抽取到函数中（如mixin）


### 12.vue如果想扩展某个现有的组件时应该怎么做？

1.使用Vue.extend直接扩展
2.使用Vue.mixin全局混入
3.HOC封装
4.可以加slot扩展



### 13.watch和computed的区别以及怎么选用?

computed：计算属性

* 计算属性是由data中的已知值，得到的一个新值。

* 这个新值只会根据已知值的变化而变化，其他不相关的数据的变化不会影响该新值。

* 计算属性不在data中，计算属性新值的相关已知值在data中。

* 别人变化影响我自己。

  

watch：监听数据的变化

* 监听data中数据的变化
* 监听的数据就是data中的已知值
* 我的变化影响别人



使用场景：

computed：　　　　
　　当一个属性受多个属性影响的时候就需要用到computed
　　最典型的例子： 购物车商品结算的时候

watch：
　　当一条数据影响多条数据的时候就需要用watch
　　最典型的例子：搜索数据



### 14.谈谈你对vue生命周期的理解？

1、我们在使用vue时必不可少的操作就是 var vm = new Vue({}),这样我们就创建了一个vue的实例对象

2、表示，刚初始化了一个vue空的实例对象，这时候，这个对象身上，只有默认的一些生命周期函数和默认的事件，其他的东西都未创建，注意，在beforeCreate生命周期函数执行的时候，data和methods中的数据都还没有初始化。

3、在created中，data和methods都已经初始化好了！//如果要调用methods中的方法或操作data中的数据，最早，只能在created中操作

4、这里表示Vue开始编辑模板，把Vue代码中的那些指令进行，最终，在内存中生成一个编译好的最终模板字符串，然后，把这个模板字符串，渲染为DOM，此时，只是在内存中，渲染好了模板，并没有把模板挂在到真正的页面中去

5、beforeMount此函数执行的时候，模板已经在内存中编译好了，但是尚未挂在到页面中去，此时，页面还是旧的

6、mounted这一步，将内存中编译好的模板，真实的替换到浏览器中去，如果要通过某些插件操作页面上的DOM节点，最早要在mounted中进行

7、只要执行完了mounted，就表示整个vue实例已经初始化完毕了，此时，组件已经脱离了创建阶段，进入到了运行阶段

8、这些时组件运行阶段的生命周期函数，只有两个，beforeupdate个updated，这俩事件，会根据data数据的改变，有选择触发0到多次

9、先根据data中最新的数据，在内存中，才重新渲染出一份最新的内存DOM树，当最新的内存DOM树被更新之后，会把最新的内存DOM树重新渲染到真实的页面中去，这时候，就完成了数据从data（Model层）->vie（视图层）的更新

10、updated事件执行的时候，页面和data数据已经保持同步了，都是最新的

11、结论：当执行beforeUpdate的时候，页面中的显示的数据，还是旧的，此时data数据是最新的，页面尚未和最新的数据保持同步

12、当执行beforeDestory钩子函数的时候，vue实例就已经从运行阶段进入到了销毁阶段：当执行beforeDestory的时候，实例身上所有的data和所有的methods，以及过滤器指令等，都处于可用状态，此时，还没有真正执行销毁的过程

13、当执行到destoryed函数的时候，组件已经被完全的销毁了，此时，组件中的数据、方法、指令、过滤器等都已经不可用了



### 15.谈谈你对vuex使用及其理解？

1.vuex是什么？
    vuex是vue框架的状态管理器。

2.如何使用？
    在main.js中引入store；新建store，引入state，const，getters，mutations，actions；

3.使用他的功能场景？
    单页应用，组件之间的状态，音乐播放，登录状态，加入购物车，定位

4.不用Vuex会带来的问题
    可维护性下降，若是修改数据就要维护三个地方；
    可读性下降，因为一个组件里的数据根本看不出来是从哪里来的；
    增加耦合，大量的上传派发会让耦合性大大增加；

5.vuex的属性
    有五种属性，State，Getter，Mutation，Action，Module。
    （1）State特性：
            存储数据，存储状态。将vuex比作一个仓库，仓库里面存放许多对象。而state就是数据源的存放地，对应vue里面的data。
            state里面存放的数据是响应式的，Vue组件从store中读取数据，若是store中的数据发生改变，依赖这个数据的组件也会发生更新。
            通过mapState把全局的state和getters映射到当前组件的computed计算属性中。
    （2）getter特性：
            对state进行计算操作，他就是store的计算属性。防止多次计算降低性能。
            可以在多组间之间复用。若是一个状态只在一个组件内使用就可以不用getters。
    （3）Mutation特性：
            被action调用。功能非常单一：只是改变state数据和状态。
    （4）Action特性：
            处理异步程序。
　（5）Module模块：
　　　　vuex允许将store分成若干模块，每个模块都可以包含以上四种属性。若调用一个变量，但是不同的模块都有的一个同名的变量，这是调用时就会出问题。解决：在模块中添加命名空间：namespaced：true；调用时采用对象的形式调用 某个模块的某个变量就可以了。例如：...Vuex.mapState({a:state=>state.homeStore.a}) ； ...mapActions({fn:"homeStore/fn"})  

6.数据流动

![image-20200212150404892](/Users/yuqirong/Library/Application Support/typora-user-images/image-20200212150404892.png)

7.辅助函数
    属性: mapState , mapGetters    在computed中
    方法: mapMutations , mapActions  在methods中

![image-20200212150504708](/Users/yuqirong/Library/Application Support/typora-user-images/image-20200212150504708.png)



### 16.你知道nextTick的原理吗？

nextTick是全局vue的一个函数，在vue系统中，用于处理dom更新的操作。vue里面有一个watcher，用于观察数据的变化，然后更新dom，vue里面并不是每次数据改变都会触发更新dom，而是将这些操作都缓存在一个队列，在一个事件循环结束之后，刷新队列，统一执行dom更新操作。 

在vue生命周期的created()钩子函数进行的DOM操作要放在Vue.nextTick()的回调函数中，因为created()钩子函数执行的时候DOM并未进行任何渲染，而此时进行DOM操作是徒劳的，所以此处一定要将DOM操作的JS代码放进Vue.nextTick()的回调函数中。

而与之对应的mounted钩子函数，该钩子函数执行时所有的DOM挂载和渲染都已完成，此时该钩子函数进行任何DOM操作都不会有个问题。 


### 17.你知道vue的双向数据绑定的原理吗？

1.vue 双向数据绑定是通过 数据劫持 结合 发布订阅模式的方式来实现的， 也就是说数据和视图同步，数据发生变化，视图跟着变化，视图变化，数据也随之发生改变；

2.核心：关于VUE双向数据绑定，其核心是 Object.defineProperty()方法；

3.介绍一下Object.defineProperty()方法：

* Object.defineProperty(obj, prop, descriptor) ，这个语法内有三个参数，分别为 obj （要定义其上属性的对象） prop （要定义或修改的属性） descriptor （具体的改变方法）
* 简单地说，就是用这个方法来定义一个值。当调用时我们使用了它里面的get方法，当我们给这个属性赋值时，又用到了它里面的set方法；



### 18.vue-router导航钩子有哪些？

1、全局守卫： router.beforeEach

2、全局解析守卫： router.beforeResolve

3、全局后置钩子： router.afterEach

4、路由独享的守卫： beforeEnter

5、组件内的守卫： beforeRouteEnter、beforeRouteUpdate (2.2 新增)、beforeRouteLeave

导航表示路由正在发生改变，vue-router 提供的导航守卫主要用来:通过跳转或取消的方式守卫导航。有多种机会植入路由导航过程中：全局的, 单个路由独享的, 或者组件级的。

注意：参数或查询的改变并不会触发进入/离开的导航守卫。 你可以通过 观察 $route 对象 来应对这些变化，或使用 beforeRouteUpdate的组件内守卫。



### 19.什么是一个递归组件？

组件在它的模板内可以递归地调用自己，只有当它有 name 选项时才可以。 在官网这句话就是关键定义组件是一定要有name属性。



### 20.谈一谈你对vue响应式原理的理解？

![image-20200212171451420](/Users/yuqirong/Library/Application Support/typora-user-images/image-20200212171451420.png)

1.把一个普通 JavaScript 对象传给 Vue 实例的 data 选项，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。

2.组件实例的 watcher 实例对象



二：创建的Vue组件实例上添加响应式属性。   解决办法：将响应属性添加到嵌套的对象上

1.Vue.set(object, key, value) 还可以使用 vm.$set 实例方法，这也是全局 Vue.set 方法的别名。

2.this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })   // 来代替 	    Object.assign(this.someObject, { a: 1, b: 2 })

 

三：异步更新队列

1.数据变化，添加到DOM更新队列。












