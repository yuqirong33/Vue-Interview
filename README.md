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



