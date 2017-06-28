### vue学习笔记

#### 1、[camelCase vs. kebab-case](https://cn.vuejs.org/v2/guide/components.html#camelCase-vs-kebab-case)
HTML 特性是不区分大小写的。所以，当使用的不是字符串模版，
camelCased (驼峰式) 命名的 prop 需要转换为相对应的 kebab-case (短横线隔开式) 命名。

#### 2、[字面量语法 vs 动态语法](https://cn.vuejs.org/v2/guide/components.html#字面量语法-vs-动态语法)
```
<!-- 传递了一个字符串 "1" -->
<comp some-prop="1"></comp>
```
因为它是一个字面 prop ，它的值是字符串 "1" 而不是number。
如果想传递一个实际的number，需要使用 v-bind ，从而让它的值被当作 JavaScript 表达式计算。
```
<!-- 传递实际的 number -->
<comp v-bind:some-prop="1"></comp>
```
#### 3、[使用 v-on 绑定自定义事件](https://cn.vuejs.org/v2/guide/components.html#使用-v-on-绑定自定义事件)

    使用 $on(eventName) 监听事件
    使用 $emit(eventName) 触发事件
    
#### 4、[使用 Slot 分发内容](https://cn.vuejs.org/v2/guide/components.html#使用-Slot-分发内容)
内容分发是个很好玩的东西，可点击上述链接。

#### 5、[keep-alive](https://cn.vuejs.org/v2/guide/components.html#keep-alive)

keep-alive可以把切换出去的组件保留在内存中，可以保留它的状态或避免重新渲染。
