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








