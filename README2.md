# Vue-Interview

### 1.v-if和v-for哪个优先级高？如果两个同时出现，应该怎么优化得到更好的性能？







### 2.Vue组件data选项为什么必须是个函数而Vue的根实例则没有此限制？

Vue组件可能存在多个实例，如果使用对象形式去定义data则会导致他们共用一个data对象，那么状态变更将会影响所有组件实例，这是不合理的；采用函数形式去定义，在initData时会将其作为工厂函数返回全新的data对象，有效的规避多实例质检的状态污染。而在Vue根实例创建过程中则不存在该限制，也是因为根实例只能有一个，不需要担心这种问题。



### 3.你知道vue中key的作用和工作原理吗？说说你对它的理解。



### 4.你怎么理解vue中的diff算法







### 5.谈一谈对vue组件化的理解？





### 6.谈一谈对vue的设计原则的理解？





### 7.vue为什么要求组件模板只能有一个根元素？



### 8.谈谈你对MVC、MVP和MVVM的理解？









### 9.谈谈你对vue组件之间通信的理解？





### 10.你了解哪些vue性能优化方法？











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











